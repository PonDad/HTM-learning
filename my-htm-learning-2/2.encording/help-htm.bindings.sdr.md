Help on module htm.bindings.sdr in htm.bindings:

NAME
    htm.bindings.sdr

CLASSES
    pybind11_builtins.pybind11_object(builtins.object)
        Metrics
        MetricsHelper_
            ActivationFrequency
            Overlap
            Sparsity
        SDR
    
    class ActivationFrequency(MetricsHelper_)
     |  Measures the activation frequency of each value in an SDR.  This accumulates
     |  measurements using an exponential moving average, and outputs a summary of
     |  results.
     |  
     |  Activation frequencies are Real numbers in the range [0, 1], where zero
     |  indicates never active, and one indicates always active.
     |  Example Usage:
     |      A = SDR( 2 )
     |      B = ActivationFrequency( A, period = 1000 )
     |      A.dense = [0, 0]
     |      A.dense = [0, 1]
     |      A.dense = [1, 1]
     |      B.activationFrequency -> { 0.33, 0.66 }
     |      B.min()     -> 1/3
     |      B.max()     -> 2/3
     |      B.mean()    -> 1/2
     |      B.std()     -> ~0.16
     |      B.entropy() -> ~0.92
     |      str(B)      -> Activation Frequency Min/Mean/Std/Max 0.333333 / 0.5 / 0.166667 / 0.666667
     |                     Entropy 0.918296
     |  
     |  Method resolution order:
     |      ActivationFrequency
     |      MetricsHelper_
     |      pybind11_builtins.pybind11_object
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __init__(...)
     |      __init__(*args, **kwargs)
     |      Overloaded function.
     |      
     |      1. __init__(self: htm.bindings.sdr.ActivationFrequency, sdr: htm.bindings.sdr.SDR, period: int, initialValue: float = -1) -> None
     |      
     |      Argument sdr is data source to track.  Add data to this ActivationFrequency
     |      instance by assigning to this SDR.
     |      
     |      Argument period is time constant for exponential moving average.
     |      
     |      Argument initialValue is Optional.  Makes this ActivationFrequency instance
     |      think that it is the result of a long running process (even though it was just
     |      created).  This assigns an initial activation frequency to all bits in the SDR,
     |      and causes it to always use the exponential moving average instead of the
     |      regular average which is usually applied to the first "period" many samples.
     |      
     |      Note: This argument is useful for using this metric as part of boosting
     |            algorithms which seek to push the activation frequencies to a target
     |            value. These algorithms will overreact to the default early behavior of
     |            this class during the first "period" many samples.
     |      
     |      
     |      2. __init__(self: htm.bindings.sdr.ActivationFrequency, dimensions: List[int], period: int, initialValue: float = -1) -> None
     |      
     |      Argument dimensions of SDR.  Add data to this ActivationFrequency
     |      instance by calling method af.addData( SDR ) with an SDR which has
     |      these dimensions.
     |      
     |      Argument period is time constant for exponential moving average.
     |  
     |  __str__(...)
     |      __str__(self: htm.bindings.sdr.ActivationFrequency) -> object
     |  
     |  entropy(...)
     |      entropy(self: htm.bindings.sdr.ActivationFrequency) -> float
     |      
     |      Binary entropy is a measurement of information.  It measures how well the
     |      SDR utilizes its resources (bits).  A low entropy indicates that many
     |      bits in the SDR are under-utilized and do not transmit as much
     |      information as they could.  A high entropy indicates that the SDR
     |      optimally utilizes its resources.  The most optimal use of SDR resources
     |      is when all bits have an equal activation frequency.  For convenience,
     |      the entropy is scaled by the theoretical maximum into the range [0, 1].
     |      
     |      Returns binary entropy of SDR, scaled to range [0, 1].
     |  
     |  max(...)
     |      max(self: htm.bindings.sdr.ActivationFrequency) -> float
     |      
     |      Maximum of Activation Frequencies
     |  
     |  mean(...)
     |      mean(self: htm.bindings.sdr.ActivationFrequency) -> float
     |      
     |      Average of Activation Frequencies
     |  
     |  min(...)
     |      min(self: htm.bindings.sdr.ActivationFrequency) -> float
     |      
     |      Minimum of Activation Frequencies
     |  
     |  std(...)
     |      std(self: htm.bindings.sdr.ActivationFrequency) -> float
     |      
     |      Standard Deviation of Activation Frequencies
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  activationFrequency
     |      Data Buffer of Activation Frequencies
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from MetricsHelper_:
     |  
     |  addData(...)
     |      addData(self: htm.bindings.sdr.MetricsHelper_, arg0: htm.bindings.sdr.SDR) -> None
     |      
     |      Add an SDR datum to this Metric.  This method can only be called if the
     |      Metric was constructed with dimensions and NOT an SDR.
     |      
     |      Argument sdr is data source, its dimensions must be the same as this Metric's
     |      dimensions.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors inherited from MetricsHelper_:
     |  
     |  dimensions
     |      Shape of the SDR data source.
     |  
     |  period
     |      Time constant for the exponential moving average which incorporate data into
     |      this measurement.  If there are fewer data samples than the period then a regular
     |      average is used instead of an exponential moving average.
     |  
     |  samples
     |      Number of data samples received & incorporated into this measurement.
     |  
     |  ----------------------------------------------------------------------
     |  Static methods inherited from pybind11_builtins.pybind11_object:
     |  
     |  __new__(*args, **kwargs) from pybind11_builtins.pybind11_type
     |      Create and return a new object.  See help(type) for accurate signature.
    
    class Metrics(pybind11_builtins.pybind11_object)
     |  Measures an SDR.  This applies the following three metrics:
     |       Sparsity
     |       ActivationFrequency
     |       Overlap
     |  This accumulates measurements using an exponential moving average, and
     |  outputs a summary of results.
     |  
     |  Example Usage:
     |      A = SDR( dimensions = 2000 )
     |      M = Metrics( A, period = 1000 )
     |      A.randomize( 0.10 )
     |      for i in range( 20 ):
     |          A.addNoise( 0.55 )
     |  
     |      M.sparsity            -> Sparsity class instance
     |      M.activationFrequency -> ActivationFrequency class instance
     |      M.overlap             -> Overlap class instance
     |      str(M) -> SDR( 2000 )
     |                  Sparsity Min/Mean/Std/Max 0.1 / 0.1 / 0 / 0.1
     |                  Activation Frequency Min/Mean/Std/Max 0 / 0.1 / 0.100464 / 0.666667
     |                  Entropy 0.822222
     |                  Overlap Min/Mean/Std/Max 0.45 / 0.45 / 0 / 0.45
     |  
     |  Method resolution order:
     |      Metrics
     |      pybind11_builtins.pybind11_object
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __init__(...)
     |      __init__(*args, **kwargs)
     |      Overloaded function.
     |      
     |      1. __init__(self: htm.bindings.sdr.Metrics, sdr: htm.bindings.sdr.SDR, period: int) -> None
     |      
     |      Argument sdr is data source to track.  Add data to this Metrics instance
     |      by assigning to this SDR.
     |      
     |      Argument period is time constant for exponential moving average.
     |      
     |      2. __init__(self: htm.bindings.sdr.Metrics, dimensions: List[int], period: int) -> None
     |      
     |      Argument dimensions of SDR.  Add data to this Metrics instance
     |      by calling method metrics.addData( SDR ) with an SDR which has these dimensions.
     |      
     |      Argument period is time constant for exponential moving average.
     |  
     |  __str__(...)
     |      __str__(self: htm.bindings.sdr.Metrics) -> object
     |  
     |  addData(...)
     |      addData(self: htm.bindings.sdr.Metrics, sdr: htm.bindings.sdr.SDR) -> None
     |      
     |      Add an SDR datum to these Metrics.  This method can only be called if
     |      Metrics was constructed with dimensions and NOT an SDR.
     |      
     |      Argument sdr is data source, its dimensions must be the same as this Metric's
     |      dimensions.
     |  
     |  reset(...)
     |      reset(self: htm.bindings.sdr.Metrics) -> None
     |      
     |      For use with time-series data sets.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  activationFrequency
     |  
     |  dimensions
     |  
     |  overlap
     |  
     |  sparsity
     |  
     |  ----------------------------------------------------------------------
     |  Static methods inherited from pybind11_builtins.pybind11_object:
     |  
     |  __new__(*args, **kwargs) from pybind11_builtins.pybind11_type
     |      Create and return a new object.  See help(type) for accurate signature.
    
    class MetricsHelper_(pybind11_builtins.pybind11_object)
     |  Method resolution order:
     |      MetricsHelper_
     |      pybind11_builtins.pybind11_object
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __init__(self, /, *args, **kwargs)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  addData(...)
     |      addData(self: htm.bindings.sdr.MetricsHelper_, arg0: htm.bindings.sdr.SDR) -> None
     |      
     |      Add an SDR datum to this Metric.  This method can only be called if the
     |      Metric was constructed with dimensions and NOT an SDR.
     |      
     |      Argument sdr is data source, its dimensions must be the same as this Metric's
     |      dimensions.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  dimensions
     |      Shape of the SDR data source.
     |  
     |  period
     |      Time constant for the exponential moving average which incorporate data into
     |      this measurement.  If there are fewer data samples than the period then a regular
     |      average is used instead of an exponential moving average.
     |  
     |  samples
     |      Number of data samples received & incorporated into this measurement.
     |  
     |  ----------------------------------------------------------------------
     |  Static methods inherited from pybind11_builtins.pybind11_object:
     |  
     |  __new__(*args, **kwargs) from pybind11_builtins.pybind11_type
     |      Create and return a new object.  See help(type) for accurate signature.
    
    class Overlap(MetricsHelper_)
     |  Measures the overlap between successive assignments to an SDR.  This class
     |  accumulates measurements using an exponential moving average, and outputs a
     |  summary of results.
     |  
     |  This class normalizes the overlap into the range [0, 1] by dividing by the
     |  number of active values.
     |  
     |  Example Usage:
     |      A = SDR( dimensions = 1000 )
     |      B = Overlap( A, period = 1000 )
     |      A.randomize( 0.20 )
     |      A.addNoise( 0.95 )  ->  5% overlap
     |      A.addNoise( 0.55 )  -> 45% overlap
     |      A.addNoise( 0.72 )  -> 28% overlap
     |      B.overlap   ->  0.28
     |      B.min()     ->  0.05
     |      B.max()     ->  0.45
     |      B.mean()    ->  0.26
     |      B.std()     -> ~0.16
     |      str(B)      -> Overlap Min/Mean/Std/Max 0.05 / 0.260016 / 0.16389 / 0.45
     |  
     |  Method resolution order:
     |      Overlap
     |      MetricsHelper_
     |      pybind11_builtins.pybind11_object
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __init__(...)
     |      __init__(*args, **kwargs)
     |      Overloaded function.
     |      
     |      1. __init__(self: htm.bindings.sdr.Overlap, sdr: htm.bindings.sdr.SDR, period: int) -> None
     |      
     |      Argument sdr is data source to track.  Add data to this Overlap instance
     |      by assigning to this SDR.
     |      
     |      Argument period is time constant for exponential moving average.
     |      
     |      2. __init__(self: htm.bindings.sdr.Overlap, dimensions: List[int], period: int) -> None
     |      
     |      Argument dimensions of SDR.  Add data to this Overlap instance
     |      by calling method overlap.addData( SDR ) with an SDR which has these dimensions.
     |      
     |      Argument period is time constant for exponential moving average.
     |  
     |  __str__(...)
     |      __str__(self: htm.bindings.sdr.Overlap) -> object
     |  
     |  max(...)
     |      max(self: htm.bindings.sdr.Overlap) -> float
     |      
     |      Maximum Overlap
     |  
     |  mean(...)
     |      mean(self: htm.bindings.sdr.Overlap) -> float
     |      
     |      Average Overlap
     |  
     |  min(...)
     |      min(self: htm.bindings.sdr.Overlap) -> float
     |      
     |      Minimum Overlap
     |  
     |  reset(...)
     |      reset(self: htm.bindings.sdr.Overlap) -> None
     |      
     |      For use with time-series data sets.
     |  
     |  std(...)
     |      std(self: htm.bindings.sdr.Overlap) -> float
     |      
     |      Standard Deviation of Overlap
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  overlap
     |      Overlap between the two most recently added SDRs.
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from MetricsHelper_:
     |  
     |  addData(...)
     |      addData(self: htm.bindings.sdr.MetricsHelper_, arg0: htm.bindings.sdr.SDR) -> None
     |      
     |      Add an SDR datum to this Metric.  This method can only be called if the
     |      Metric was constructed with dimensions and NOT an SDR.
     |      
     |      Argument sdr is data source, its dimensions must be the same as this Metric's
     |      dimensions.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors inherited from MetricsHelper_:
     |  
     |  dimensions
     |      Shape of the SDR data source.
     |  
     |  period
     |      Time constant for the exponential moving average which incorporate data into
     |      this measurement.  If there are fewer data samples than the period then a regular
     |      average is used instead of an exponential moving average.
     |  
     |  samples
     |      Number of data samples received & incorporated into this measurement.
     |  
     |  ----------------------------------------------------------------------
     |  Static methods inherited from pybind11_builtins.pybind11_object:
     |  
     |  __new__(*args, **kwargs) from pybind11_builtins.pybind11_type
     |      Create and return a new object.  See help(type) for accurate signature.
    
    class SDR(pybind11_builtins.pybind11_object)
     |  Sparse Distributed Representation
     |  
     |  This class manages the specification and momentary value of a Sparse Distributed
     |  Representation (SDR).  An SDR is a group of boolean values which represent the
     |  state of a group of neurons or their associated processes.
     |  
     |  SDR's have three commonly used data formats which are:
     |  *   dense
     |  *   sparse
     |  *   coordinates
     |  The SDR class has three magic properties, one for each of these data formats.
     |  These properties are the primary way of accessing the SDR's data.  When these
     |  properties are read from, the data is automatically converted to the requested
     |  format and is cached so getting a value in one format many times incurs no extra
     |  performance cost.  Assigning to the SDR via any one of these properties clears
     |  the cached values and causes them to be recomputed as needed.
     |  
     |  Example usage:
     |      # Make an SDR with 9 values, arranged in a (3 x 3) grid.
     |      X = SDR(dimensions = (3, 3))
     |  
     |      # These three statements are equivalent.
     |      X.dense  = [[0, 1, 0],
     |                  [0, 1, 0],
     |                  [0, 0, 1]]
     |      X.sparse = [ 1, 4, 8 ]
     |      X.coordinates = [[0, 1, 2], [1, 1, 2]]
     |  
     |      # Access data in any format, SDR will automatically convert data formats,
     |      # even if it was not the format used by the most recent assignment to the
     |      # SDR.
     |      X.dense  -> [[ 0, 1, 0 ],
     |                   [ 0, 1, 0 ],
     |                   [ 0, 0, 1 ]]
     |      x.sparse -> [ 1, 4, 8 ]
     |      X.coordinates -> [[ 0, 1, 2 ], [1, 1, 2 ]]
     |  
     |      # Data format conversions are cached, and when an SDR value changes the
     |      # cache is cleared.
     |      X.sparse = [1, 2, 3] # Assign new data to the SDR, clearing the cache.
     |      X.dense     # This line will convert formats.
     |      X.dense     # This line will resuse the result of the previous line
     |  
     |  Assigning a value to the SDR requires copying the data from Python into C++. To
     |  avoid this copy operation: modify sdr.dense inplace, and assign it to itself.
     |  This class will detect that it's being given it's own data and will omit the
     |  copy operation.
     |  
     |  Example Usage of In-Place Assignment:
     |      X    = SDR((1000, 1000))   # Initial value is all zeros
     |      data = X.dense
     |      data[  0,   4] = 1
     |      data[444, 444] = 1
     |      X.dense = data
     |      X.sparse -> [ 4, 444444 ]
     |  
     |  Data Validity Warning:  After assigning a new value to the SDR, all existing
     |  numpy arrays of data are invalid.  In order to get the latest copy of the data,
     |  re-access the data from the SDR.  Examples:
     |      A = SDR( dimensions )
     |      out_of_date = A.dense
     |      A.sparse = []
     |      # The variable "out_of_date" is now liable to be overwritten.
     |      A.dense = out_of_date   # This does not work, since the data is invalid.
     |  
     |  Method resolution order:
     |      SDR
     |      pybind11_builtins.pybind11_object
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __eq__(...)
     |      __eq__(self: htm.bindings.sdr.SDR, arg0: htm.bindings.sdr.SDR) -> bool
     |  
     |  __getstate__(...)
     |      __getstate__(self: htm.bindings.sdr.SDR) -> bytes
     |  
     |  __init__(...)
     |      __init__(*args, **kwargs)
     |      Overloaded function.
     |      
     |      1. __init__(self: htm.bindings.sdr.SDR, dimensions: List[int]) -> None
     |      
     |      Create an SDR object.  The initial value is all zeros.
     |      
     |      Argument dimensions is a list of dimension sizes, defining the shape of the SDR.
     |      The product of the dimensions must be greater than zero.
     |      
     |      2. __init__(self: htm.bindings.sdr.SDR, dimensions: int) -> None
     |      
     |      Create an SDR object.  The initial value is all zeros.
     |      
     |      Argument dimensions is a single integer dimension size, defining a 1-dimensional
     |      SDR.  Must be greater than zero.
     |      
     |      3. __init__(self: htm.bindings.sdr.SDR, sdr: htm.bindings.sdr.SDR) -> None
     |      
     |      Initialize this SDR as a deep copy of the given SDR.  This SDR and the given
     |      SDR will have no shared data and they can be modified without affecting each
     |      other.
     |  
     |  __ne__(...)
     |      __ne__(self: htm.bindings.sdr.SDR, arg0: htm.bindings.sdr.SDR) -> bool
     |  
     |  __setstate__(...)
     |      __setstate__(self: htm.bindings.sdr.SDR, arg0: bytes) -> None
     |  
     |  __str__(...)
     |      __str__(self: htm.bindings.sdr.SDR) -> object
     |  
     |  addNoise(...)
     |      addNoise(self: htm.bindings.sdr.SDR, fractionNoise: float, seed: int = 0) -> htm.bindings.sdr.SDR
     |      
     |      Modify the SDR by moving a fraction of the active bits to different
     |      locations.  This method does not change the sparsity of the SDR, it moves
     |      the locations of the true values.  The resulting SDR has a controlled
     |      amount of overlap with the original.
     |      
     |      Argument fractionNoise is the fraction of active bits to swap out.  The original
     |      and resulting SDRs have the following relationship:
     |          originalSDR.getOverlap( newSDR ) / sparsity == 1 - fractionNoise
     |      
     |      Optional argument seed is used for the random number generator.  Seed 0 is
     |      special, it is replaced with the system time.  The default seed is 0.
     |  
     |  concatenate(...)
     |      concatenate(*args, **kwargs)
     |      Overloaded function.
     |      
     |      1. concatenate(self: htm.bindings.sdr.SDR, input1: htm.bindings.sdr.SDR, input2: htm.bindings.sdr.SDR, axis: int = 0) -> htm.bindings.sdr.SDR
     |      
     |      Concatenates SDRs and stores the result in this SDR.
     |      
     |      This method has two overloads:
     |          1) Accepts two SDRs, for convenience.
     |          2) Accepts a list of SDRs, must contain at least two SDRs, can
     |             contain as many SDRs as needed.
     |      
     |      Argument axis: This can concatenate along any axis, as long as the
     |      result has the same dimensions as this SDR.  The default axis is 0.
     |      
     |      The output is stored in this SDR.  This method modifies this SDR
     |      and discards its current value!
     |      
     |      Example Usage:
     |          A = SDR( 10 )
     |          B = SDR( 10 )
     |          C = SDR( 20 )
     |          A.sparse = [0, 1, 2]
     |          B.sparse = [0, 1, 2]
     |          C.concatenate( A, B )
     |          C.sparse == [0, 1, 2, 10, 11, 12]
     |      
     |      
     |      2. concatenate(self: htm.bindings.sdr.SDR, inputs: List[htm.bindings.sdr.SDR], axis: int = 0) -> htm.bindings.sdr.SDR
     |  
     |  flatten(...)
     |      flatten(self: htm.bindings.sdr.SDR) -> htm.bindings.sdr.SDR
     |      
     |      Change the dimensions of the SDR into one big dimension.
     |  
     |  getOverlap(...)
     |      getOverlap(self: htm.bindings.sdr.SDR, arg0: htm.bindings.sdr.SDR) -> int
     |      
     |      Calculates the number of true bits which both SDRs have in common.
     |  
     |  getSparsity(...)
     |      getSparsity(self: htm.bindings.sdr.SDR) -> float
     |      
     |      Calculates the sparsity of the SDR, which is the fraction of bits which are
     |      true out of the total number of bits in the SDR.
     |      I.E.  sparsity = sdr.getSum() / sdr.size
     |  
     |  getSum(...)
     |      getSum(self: htm.bindings.sdr.SDR) -> int
     |      
     |      Calculates the number of true values in the SDR.
     |  
     |  intersection(...)
     |      intersection(*args, **kwargs)
     |      Overloaded function.
     |      
     |      1. intersection(self: htm.bindings.sdr.SDR, arg0: htm.bindings.sdr.SDR, arg1: htm.bindings.sdr.SDR) -> htm.bindings.sdr.SDR
     |      
     |      This method calculates the set intersection of the active bits in each input
     |      SDR.
     |      
     |      This method has two overloads:
     |          1) Accepts two SDRs, for convenience.
     |          2) Accepts a list of SDRs, must contain at least two SDRs, can contain as
     |             many SDRs as needed.
     |      
     |      In both cases the output is stored in this SDR.  This method modifies this SDR
     |      and discards its current value!
     |      
     |      Example Usage:
     |          A = SDR( 10 )
     |          B = SDR( 10 )
     |          X = SDR( 10 )
     |          A.sparse = [0, 1, 2, 3]
     |          B.sparse =       [2, 3, 4, 5]
     |          X.intersection( A, B )
     |          X.sparse -> [2, 3]
     |      
     |      
     |      2. intersection(self: htm.bindings.sdr.SDR, arg0: List[htm.bindings.sdr.SDR]) -> htm.bindings.sdr.SDR
     |  
     |  killCells(...)
     |      killCells(self: htm.bindings.sdr.SDR, fraction: float, seed: int = 0) -> htm.bindings.sdr.SDR
     |      
     |      Modify the SDR by setting a fraction of the bits to zero.
     |      
     |      Argument fraction must be between 0 and 1 (inclusive).  This fraction of the
     |      cells in the SDR will be set to zero, regardless of their current state.
     |      
     |      Argument seed is for a random number generator.  If not given, this uses the
     |      magic seed 0.  Use the same seed to consistently kill the same cells.
     |  
     |  randomize(...)
     |      randomize(*args, **kwargs)
     |      Overloaded function.
     |      
     |      1. randomize(self: htm.bindings.sdr.SDR, sparsity: float, seed: int = 0) -> htm.bindings.sdr.SDR
     |      
     |      Make a random SDR, overwriting the current value of the SDR.  The result has
     |      uniformly random activations.
     |      
     |      Argument sparsity is the fraction of bits to set to true.  After calling this
     |      method sdr.getSparsity() will return this sparsity, rounded to the nearest
     |      fraction of self.size.
     |      
     |      Optional argument seed is used for the random number generator.  Seed 0 is
     |      special, it is replaced with the system time  The default seed is 0.
     |      
     |      2. randomize(self: htm.bindings.sdr.SDR, sparsity: float, rng: htm.bindings.math.Random) -> htm.bindings.sdr.SDR
     |      
     |      This overload accepts Random Number Generators (RNG) intead of a random seed.
     |      RNGs must be instances of "htm.bindings.math.Random".
     |  
     |  reshape(...)
     |      reshape(self: htm.bindings.sdr.SDR, arg0: List[int]) -> htm.bindings.sdr.SDR
     |      
     |      Change the dimensions of the SDR.  The total size must not change.
     |  
     |  setSDR(...)
     |      setSDR(self: htm.bindings.sdr.SDR, arg0: htm.bindings.sdr.SDR) -> htm.bindings.sdr.SDR
     |      
     |      Deep Copy the given SDR to this SDR.  This overwrites the current value of this
     |      SDR.  This SDR and the given SDR will have no shared data and they can be
     |      modified without affecting each other.
     |  
     |  union(...)
     |      union(*args, **kwargs)
     |      Overloaded function.
     |      
     |      1. union(self: htm.bindings.sdr.SDR, arg0: htm.bindings.sdr.SDR, arg1: htm.bindings.sdr.SDR) -> htm.bindings.sdr.SDR
     |      
     |      This method calculates the set union of the active bits in each input SDR.
     |      
     |      The output is stored in this SDR.  This method discards the SDRs current value!
     |      
     |      Example Usage:
     |          A = SDR( 10 )
     |          B = SDR( 10 )
     |          U = SDR( 10 )
     |          A.sparse = [0, 1, 2, 3]
     |          B.sparse =       [2, 3, 4, 5]
     |          U.union( A, B )
     |          U.sparse -> [0, 1, 2, 3, 4, 5]
     |      
     |      
     |      2. union(self: htm.bindings.sdr.SDR, arg0: List[htm.bindings.sdr.SDR]) -> htm.bindings.sdr.SDR
     |  
     |  zero(...)
     |      zero(self: htm.bindings.sdr.SDR) -> htm.bindings.sdr.SDR
     |      
     |      Set all of the values in the SDR to false.  This method overwrites the SDRs
     |      current value.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  coordinates
     |      List of numpy arrays, containing the coordinates of only the true values in
     |      the SDR.  This is a list of lists: the outter list contains an entry for each
     |      dimension in the SDR. The inner lists contain the coordinates of each true bit.
     |      The inner lists run in parallel. This format is useful because it contains the
     |      location of each true bit inside of the SDR's dimensional space.
     |      
     |      Coordinate data must be sorted and contain no duplicates.
     |  
     |  dense
     |      A numpy array of boolean values, representing all of the bits in the SDR.
     |      This format allows random-access queries of the SDRs values.
     |      
     |      After modifying this array you MUST assign the array back into the SDR, in order
     |      to notify the SDR that its dense array has changed and its cached data is out of
     |      date.  If you did't copy this data, then SDR won't copy either.
     |  
     |  dimensions
     |      A list of dimensions of the SDR.
     |  
     |  size
     |      The total number of boolean values in the SDR.
     |  
     |  sparse
     |      A numpy array containing the indices of only the true values in the SDR.
     |      These are indices into the flattened SDR. This format allows for quickly
     |      accessing all of the true bits in the SDR.
     |      
     |      Sparse data must contain no duplicates.
     |  
     |  ----------------------------------------------------------------------
     |  Static methods inherited from pybind11_builtins.pybind11_object:
     |  
     |  __new__(*args, **kwargs) from pybind11_builtins.pybind11_type
     |      Create and return a new object.  See help(type) for accurate signature.
    
    class Sparsity(MetricsHelper_)
     |  Measures the sparsity of an SDR.  This accumulates measurements using an
     |  exponential moving average, and outputs a summary of results.
     |  
     |  Example Usage:
     |      A = SDR( dimensions )
     |      B = Sparsity( A, period = 1000 )
     |      A.randomize( 0.01 )
     |      A.randomize( 0.15 )
     |      A.randomize( 0.05 )
     |      B.sparsity ->  0.05
     |      B.min()    ->  0.01
     |      B.max()    ->  0.15
     |      B.mean()   -> ~0.07
     |      B.std()    -> ~0.06
     |      str(B)     -> Sparsity Min/Mean/Std/Max 0.01 / 0.0700033 / 0.0588751 / 0.15
     |  
     |  Method resolution order:
     |      Sparsity
     |      MetricsHelper_
     |      pybind11_builtins.pybind11_object
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __init__(...)
     |      __init__(*args, **kwargs)
     |      Overloaded function.
     |      
     |      1. __init__(self: htm.bindings.sdr.Sparsity, sdr: htm.bindings.sdr.SDR, period: int) -> None
     |      
     |      Argument sdr is data source is to track.  Add data to this sparsity metric by
     |      assigning to this SDR.
     |      
     |      Argument period is time constant for exponential moving average.
     |      
     |      2. __init__(self: htm.bindings.sdr.Sparsity, dimensions: List[int], period: int) -> None
     |      
     |      Argument dimensions of SDR.  Add data to this sparsity metric by calling method
     |      sparsity.addData( SDR ) with an SDR which has these dimensions.
     |      
     |      Argument period is time constant for exponential moving average.
     |  
     |  __str__(...)
     |      __str__(self: htm.bindings.sdr.Sparsity) -> object
     |  
     |  max(...)
     |      max(self: htm.bindings.sdr.Sparsity) -> float
     |      
     |      Maximum Sparsity
     |  
     |  mean(...)
     |      mean(self: htm.bindings.sdr.Sparsity) -> float
     |      
     |      Average of Sparsity
     |  
     |  min(...)
     |      min(self: htm.bindings.sdr.Sparsity) -> float
     |      
     |      Minimum Sparsity
     |  
     |  std(...)
     |      std(self: htm.bindings.sdr.Sparsity) -> float
     |      
     |      Standard Deviation of Sparsity
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  sparsity
     |      Current Sparsity, or sparsity of most recently added SDR.
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from MetricsHelper_:
     |  
     |  addData(...)
     |      addData(self: htm.bindings.sdr.MetricsHelper_, arg0: htm.bindings.sdr.SDR) -> None
     |      
     |      Add an SDR datum to this Metric.  This method can only be called if the
     |      Metric was constructed with dimensions and NOT an SDR.
     |      
     |      Argument sdr is data source, its dimensions must be the same as this Metric's
     |      dimensions.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors inherited from MetricsHelper_:
     |  
     |  dimensions
     |      Shape of the SDR data source.
     |  
     |  period
     |      Time constant for the exponential moving average which incorporate data into
     |      this measurement.  If there are fewer data samples than the period then a regular
     |      average is used instead of an exponential moving average.
     |  
     |  samples
     |      Number of data samples received & incorporated into this measurement.
     |  
     |  ----------------------------------------------------------------------
     |  Static methods inherited from pybind11_builtins.pybind11_object:
     |  
     |  __new__(*args, **kwargs) from pybind11_builtins.pybind11_type
     |      Create and return a new object.  See help(type) for accurate signature.

FILE
    /usr/local/lib/python3.7/site-packages/htm.core-2.1.1-py3.7-macosx-10.14-x86_64.egg/htm/bindings/sdr.cpython-37m-darwin.so

