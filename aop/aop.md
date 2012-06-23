!SLIDE bullets incremental transition=scrollLeft
# AOP
* <div class='quote'>In Smalltalk, everything happens somewhere else.<br />— Adele Goldberg</div>
* making things happen elsewhere
* persisting objects<br />when things happen to them
* logging with [RCapture](https://code.google.com/p/rcapture/)

!SLIDE transition=scrollLeft
    @@@ Ruby
    class PrimeSelector
      def initialize numbers
        @numbers = numbers
      end










    end

!SLIDE
    @@@ Ruby
    class PrimeSelector
      def initialize numbers
        @numbers = numbers
      end

      def primes
        @numbers.select { |number| prime? number }
      end






    end

!SLIDE
    @@@ Ruby
    class PrimeSelector
      def initialize numbers
        @numbers = numbers
      end

      def primes
        @numbers.select { |number| prime? number }
      end

      private

      def prime? number
        # check primality of number
      end
    end

!SLIDE transition=scrollLeft
    @@@ Ruby
    require 'logger'
    require 'rcapture'

    class Logging
      def initialize log
        @log = Logger.new log
        add_logging
      end









    end

!SLIDE
    @@@ Ruby
    require 'logger'
    require 'rcapture'

    class Logging
      def initialize log
        @log = Logger.new log
        add_logging
      end

      private

      def add_logging
        PrimeSelector.class_eval { include RCapture::Interceptable }



      end
    end

!SLIDE
    @@@ Ruby
    require 'logger'
    require 'rcapture'

    class Logging
      def initialize log
        @log = Logger.new log
        add_logging
      end

      private

      def add_logging
        PrimeSelector.class_eval { include RCapture::Interceptable }
        PrimeSelector.capture_pre methods: :prime? do |point|
          @log.debug "prime? #{point.args.first}"
        end
      end
    end

!SLIDE transition=scrollLeft
    @@@ Ruby
    Logging.new $stdout
    PrimeSelector.new(1..7).primes

    # D, [2012-06-23T22:52:48.718999 #5870] DEBUG -- : prime? 1
    # D, [2012-06-23T22:52:48.720303 #5870] DEBUG -- : prime? 2
    # D, [2012-06-23T22:52:48.720385 #5870] DEBUG -- : prime? 3
    # D, [2012-06-23T22:52:48.720459 #5870] DEBUG -- : prime? 4
    # D, [2012-06-23T22:52:48.720534 #5870] DEBUG -- : prime? 5
    # D, [2012-06-23T22:52:48.720638 #5870] DEBUG -- : prime? 6
    # D, [2012-06-23T22:52:48.720731 #5870] DEBUG -- : prime? 7

!SLIDE bullets incremental transition=scrollLeft
# AOP
* work with you objects<br />as if the memory was forever
* make a separate presistence layer<br />that hooks into state-changing methods
* …or explicitly route through that layer<br />and make it persist the changes afterwards
