### Design a parking
```
// wrong example
class ParkingLot {
    fields: data that can be quantified.
    int total_slots[];
    int taken_slots[];
    int empty_slots[];
    double parking_fee_per_hour;

}
```

Design a Parking Lot
1. General steps for OOD
2. Basic design
3. Extension

Steps:
1. Understand/Analyze the use case.(specify the function of the program)

Use case: Describe the parking lot building？ Vehicle monitoring? What kind of parking lot?

Design doc

Use cases -> API (application programming interface)
For API, always ask yourself: input/output?

### Some other questions that may affect your design:
- One level or multiple levels? **Multiple Levels**
- Do we need different type of slots? **No**
- Parking-Spot / Vehicle sizes? **Compact, full**
- Tracking the location of each vehicle? **No**
- Charge a fee? **No**

海龟汤

2. Classes and their relationships
- Single-responsibility Principle: A class should have only one job

vehicle, Parking spot, level, parkinglot...

### class relationships:
- Association: a general binary relationship that describes and activity between two classes.
- Aggregation/Composition: a special form of association, which represents an ownership relationship between two classes. (has-a)
- Difference: can they exist independently

### Inheritance(is a)

- Parking Lot -- Level (has-a, aggregation/composition)
- Level -- Parking Spot (has-a, aggregation/composition)
- Vehicle -- Parking Spot(association)
- Vehicle -- Car, Truck (inheritance)
- Parking spot -- full-size, compact(inheritance)

#### Q: which design do you prefer?
1. ParkingLot -- Level -- ParkingSpot
- can be expanded
- relative complicated
2. ParkingLot -- ParkingSpot:
- simple!
- easy to implement

* *必须灵活运用，变通！*

- *文无第一，武无第二*

3. For complicated designs, first focus on public methods(APIs): How do others use your program?
We can discuss implementation details later.

- functionality:
    - Basic functionality: for a given vehicle, tell whether there is available spot in the parking lot.
    - Possible extensions: provide available spot locations, assign spot to the vehicle,...

    ```Java
    public class ParkingLot {
        private Level[] levels;
        /** given a vehicle, tell me whether I can park it.*/
        public boolean hasSpot(Vehicle v) {
            // TO DO: check each level, for each level, call Level#hasSpot(Vehicle)
        }

        // Return a plat_number
        boolean park(Vehicle v);
        Vehicle leave(String plate_number);
    }

    class Level {
        // tracking Parking Spots
        boolean hasSpot(Vehicle);
    }

    class ParkingSpot {   // inside the package can see
        boolean fit(Vehicle); // check size and availability
    }

    public abstract class Vehicle {
        // data fields
        // getSize() method
    }

    Car, Truck, ... extends Vehicle
    ```
4. Complete implementation
Assumption:
- multiple Levels
- Check vehicle sizes

enum可以加属性
