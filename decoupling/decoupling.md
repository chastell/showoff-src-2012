!SLIDE bullets incremental transition=scrollLeft
# going way overboard (?)
* it’s all about objects
* why not hide persistance altogether?
* [Candy](https://github.com/SFEley/candy)
* [Ambition](http://defunkt.io/ambition)

!SLIDE transition=scrollLeft
## Candy: transparent persistence in MongoDB
    @@@ Ruby
    require 'candy'













     

!SLIDE
## Candy: transparent persistence in MongoDB
    @@@ Ruby
    require 'candy'

    class Conference
      include Candy::Piece
    end









     

!SLIDE
## Candy: transparent persistence in MongoDB
    @@@ Ruby
    require 'candy'

    class Conference
      include Candy::Piece
    end

    src = Conference.new
    # connects to localhost:27017 and ‘chastell’ db if needed
    # and saves a new document to the ‘Conference’ collection





     

!SLIDE
## Candy: transparent persistence in MongoDB
    @@@ Ruby
    require 'candy'

    class Conference
      include Candy::Piece
    end

    src = Conference.new
    # connects to localhost:27017 and ‘chastell’ db if needed
    # and saves a new document to the ‘Conference’ collection

    src.location = 'Edinburgh'   # method_missing resaves



     

!SLIDE
## Candy: transparent persistence in MongoDB
    @@@ Ruby
    require 'candy'

    class Conference
      include Candy::Piece
    end

    src = Conference.new
    # connects to localhost:27017 and ‘chastell’ db if needed
    # and saves a new document to the ‘Conference’ collection

    src.location = 'Edinburgh'   # method_missing resaves

    src.events = { parties: { saturday: 'Zoë Keating concert' } }
    src.events.parties.saturday    #=> 'Zoë Keating concert'
     

!SLIDE transition=scrollLeft
## Ambition: persistence queries in Ruby
    @@@ Ruby
    require 'ambition/adapters/active_record'













     

!SLIDE
## Ambition: persistence queries in Ruby
    @@@ Ruby
    require 'ambition/adapters/active_record'

    class Person < ActiveRecord::Base
    end










     

!SLIDE
## Ambition: persistence queries in Ruby
    @@@ Ruby
    require 'ambition/adapters/active_record'

    class Person < ActiveRecord::Base
    end

    Person.select do |p|
      (p.country == 'USA' && p.age >= 21) ||
      (p.country != 'USA' && p.age >= 18)
    end





     

!SLIDE
## Ambition: persistence queries in Ruby
    @@@ Ruby
    require 'ambition/adapters/active_record'

    class Person < ActiveRecord::Base
    end

    Person.select do |p|
      (p.country == 'USA' && p.age >= 21) ||
      (p.country != 'USA' && p.age >= 18)
    end

    # SELECT * FROM people
    # WHERE (
    #   (people.country =  'USA' AND people.age >= 21) OR
    #   (people.country <> 'USA' AND people.age >= 18)
    # )

!SLIDE
## Ambition: persistence queries in Ruby
    @@@ Ruby
    require 'ambition/adapters/active_ldap'

    class Person < ActiveLdap::Base
    end

    Person.select do |p|
      (p.country == 'USA' && p.age >= 21) ||
      (p.country != 'USA' && p.age >= 18)
    end

    # (|
    #   (& (country=USA)    (age>=21) )
    #   (& (!(country=USA)) (age>=18) )
    # )
     

!SLIDE center transition=scrollRight
![giraffe](giraffe.jpg)
[giraffes of iwo jima](http://www.johnnycheeseburger.com/post/1528439687)
