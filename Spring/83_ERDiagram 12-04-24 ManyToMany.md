**Many to many Mapping**

![alt text](https://i.ibb.co/QJ9T0jz/image.png)

* create entity for bus and bus stop

```java
@Getter
@Setter
@Entity
@Table(name = "bus_stop")
public class BusStop {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id", nullable = false)
    private Long id;

    @Column(name = "stop_name", nullable = false)
    private String stopName;

}
```

* we can create mapping in 2 way
* for now we create mapping in bus entity class
* go to bus entity , in jpa designer select association

![alt text](https://i.ibb.co/mhRdQRz/image.png)

```java
@Getter
@Setter
@Entity
@Table(name = "bus")
public class Bus {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id", nullable = false)
    private Long id;

    @Column(name = "bus_name", nullable = false)
    private String busName;

    @ManyToMany
    @JoinTable(name = "bus_journry",
            joinColumns = @JoinColumn(name = "bus_id"),
            inverseJoinColumns = @JoinColumn(name = "busStops_id"))
    private Set<BusStop> busStops = new LinkedHashSet<>();

}

```
**@ManyToMany**
* ManyToMany , here first many indicates to Bus and last many indicates to BusStop
* last one decides what kind of variable is this  

![alt text](https://i.ibb.co/t34fspT/image.png)

![alt text](https://i.ibb.co/6gpcPLZ/image.png)

![alt text](https://i.ibb.co/ZY87S40/image.png)

* we can use as a list 
* in list values can be duplicate 
* but in set values cannot be duplicate

**@JoinTable(name = "bus_journry",
            joinColumns = @JoinColumn(name = "bus_id"),
            inverseJoinColumns = @JoinColumn(name = "busStops_id"))**
* this will automatically create a third table called "bus_journry" and in that it will create 2 foreign keys 
* "bus_id" , this foreign key is for the Bus 
* "busStops_id" , this foreign key is for the BusStop
* now when we start the project, it will create 3 table, one for bus, 2nd for bus_stop and 3rd table will create bus_journey for joining both tables

Now create Controller Layer

```java
package com.mapping.controller;

import com.mapping.entity.Bus;
import com.mapping.repository.BusRepository;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api/v1/bus")
public class BusController {

    private BusRepository busRepository;

    public BusController(BusRepository busRepository) {
        this.busRepository = busRepository;
    }

    @PostMapping
    public ResponseEntity<Bus> addBus(@RequestBody Bus bus) {
        return ResponseEntity.ok(busRepository.save(bus));
    }

}

```
Run the application
Now we supply the JSON data in bwlow format

```JSON
{
  "busName": "Route 101",
  "busStops": [
    {
        "id":1,
      "stopName": "Location A"
    },
    {
        "id":2,
      "stopName": "Location B"
    },
    {
        "id":3,
      "stopName": "Location C"
    }
  ]
}
```

![img](https://i.ibb.co/Przprp5/image.png)

**How to add an extra column in many to many mapping**

Many to many mapping mekes complex while implimentation

* when we create many to many relation , the third table creates automatically 
* because of automatic table creation,adding column will meke the implimentation tough.
* so we create 2 tables, and join the both table using 3rd table in oneToMany , oneToMany

![alt text](https://i.ibb.co/413WwLF/image.png)

