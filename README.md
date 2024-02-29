
Got it. Let's adjust the test class accordingly:

```java
package com.cognizant.test;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.TestEntityManager;

import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;

@DataJpaTest
public class TestSimlesRepository {

    @Autowired
    private SimlesRepository simlesRepository;

    @Autowired
    private TestEntityManager entityManager;

    @Test
    public void testFindAllPositive() {
        Simles simles = new Simles();
        simles.setSimleId(1);
        simles.setRpId("RP001"); // Assuming RP001 exists as a valid foreign key
        simles.setSource("Source");
        simles.setDestination("Destination");
        simles.setOccupancy(3);
        entityManager.persist(simles);

        Iterable<Simles> it = simlesRepository.findAll();
        assertTrue(it.iterator().hasNext());
    }

    @Test
    public void testFindAllNegative() {
        Iterable<Simles> it = simlesRepository.findAll();
        assertFalse(it.iterator().hasNext());
    }

    @Test
    public void testFindBySmileIdPositive() {
        Simles simles = new Simles();
        simles.setSimleId(1);
        simles.setRpId("RP001"); // Assuming RP001 exists as a valid foreign key
        simles.setSource("Source");
        simles.setDestination("Destination");
        simles.setOccupancy(3);
        entityManager.persist(simles);

        Optional<Simles> foundSimles = simlesRepository.findBySmileId(1);
        assertTrue(foundSimles.isPresent());
    }

    @Test
    public void testFindBySmileIdNegative() {
        Optional<Simles> notFoundSimles = simlesRepository.findBySmileId(9999);
        assertFalse(notFoundSimles.isPresent());
    }

    @Test
    public void testSavePositive() {
        Simles simles = new Simles();
        simles.setSimleId(1);
        simles.setRpId("RP001"); // Assuming RP001 exists as a valid foreign key
        simles.setSource("Source");
        simles.setDestination("Destination");
        simles.setOccupancy(3);
        simlesRepository.save(simles);

        Optional<Simles> savedSimles = simlesRepository.findBySmileId(1);
        assertTrue(savedSimles.isPresent());
    }

    @Test
    public void testDeletePositive() {
        Simles simles = new Simles();
        simles.setSimleId(1);
        simles.setRpId("RP001"); // Assuming RP001 exists as a valid foreign key
        simles.setSource("Source");
        simles.setDestination("Destination");
        simles.setOccupancy(3);
        entityManager.persist(simles);

        simlesRepository.delete(simles);

        Optional<Simles> deletedSimles = simlesRepository.findBySmileId(1);
        assertFalse(deletedSimles.isPresent());
    }

    // Add more test methods as needed
}
```

Let me know if you need any further adjustments!





package com.cognizant.test;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.TestEntityManager;

import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;

@DataJpaTest
public class TestSimlesRepository {

    @Autowired
    private SimlesRepository simlesRepository;

    @Autowired
    private TestEntityManager entityManager;

    @Test
    public void testFindAllPositive() {
        Simles simles = new Simles();
        simles.setSimleId(1);
        simles.setRpId("RP001");
        simles.setSource("Source");
        simles.setDestination("Destination");
        simles.setOccupancy(3);
        entityManager.persist(simles);

        Iterable<Simles> it = simlesRepository.findAll();
        assertTrue(it.iterator().hasNext());
    }

    @Test
    public void testFindAllNegative() {
        Iterable<Simles> it = simlesRepository.findAll();
        assertFalse(it.iterator().hasNext());
    }

    @Test
    public void testFindByRpIdPositive() {
        Simles simles = new Simles();
        simles.setSimleId(1);
        simles.setRpId("RP001");
        simles.setSource("Source");
        simles.setDestination("Destination");
        simles.setOccupancy(3);
        entityManager.persist(simles);

        Optional<Simles> foundSimles = simlesRepository.findByRpId("RP001");
        assertTrue(foundSimles.isPresent());
    }

    @Test
    public void testFindByRpIdNegative() {
        Optional<Simles> notFoundSimles = simlesRepository.findByRpId("InvalidRpId");
        assertFalse(notFoundSimles.isPresent());
    }

    @Test
    public void testSavePositive() {
        Simles simles = new Simles();
        simles.setSimleId(1);
        simles.setRpId("RP001");
        simles.setSource("Source");
        simles.setDestination("Destination");
        simles.setOccupancy(3);
        simlesRepository.save(simles);

        Optional<Simles> savedSimles = simlesRepository.findById(1);
        assertTrue(savedSimles.isPresent());
    }

    @Test
    public void testDeletePositive() {
        Simles simles = new Simles();
        simles.setSimleId(1);
        simles.setRpId("RP001");
        simles.setSource("Source");
        simles.setDestination("Destination");
        simles.setOccupancy(3);
        entityManager.persist(simles);

        simlesRepository.delete(simles);

        Optional<Simles> deletedSimles = simlesRepository.findById(1);
        assertFalse(deletedSimles.isPresent());
    }

    // Add more test methods as needed
}








Here's the updated test class with additional test methods:

```java
package com.cognizant.test;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.TestEntityManager;

import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;

@DataJpaTest
public class SmileTest {

    @Autowired
    private SmileRepository smileRepository;

    @Autowired
    private TestEntityManager entityManager;

    @Test
    public void testFindAllPositive() {
        Smile smile = new Smile();
        smile.setSmileId(1);
        smile.setRpId("RP001");
        smile.setSource("Source");
        smile.setDestination("Destination");
        smile.setOccupancy(3);
        entityManager.persist(smile);

        Iterable<Smile> it = smileRepository.findAll();
        assertTrue(it.iterator().hasNext());
    }

    @Test
    public void testFindAllNegative() {
        Iterable<Smile> it = smileRepository.findAll();
        assertFalse(it.iterator().hasNext());
    }

    @Test
    public void testFindByRpIdPositive() {
        Smile smile = new Smile();
        smile.setSmileId(1);
        smile.setRpId("RP001");
        smile.setSource("Source");
        smile.setDestination("Destination");
        smile.setOccupancy(3);
        entityManager.persist(smile);

        Optional<Smile> foundSmile = smileRepository.findByRpId("RP001");
        assertTrue(foundSmile.isPresent());
    }

    @Test
    public void testFindByRpIdNegative() {
        Optional<Smile> notFoundSmile = smileRepository.findByRpId("InvalidRpId");
        assertFalse(notFoundSmile.isPresent());
    }

    @Test
    public void testSavePositive() {
        Smile smile = new Smile();
        smile.setSmileId(1);
        smile.setRpId("RP001");
        smile.setSource("Source");
        smile.setDestination("Destination");
        smile.setOccupancy(3);
        smileRepository.save(smile);

        Optional<Smile> savedSmile = smileRepository.findById(1);
        assertTrue(savedSmile.isPresent());
    }

    @Test
    public void testDeletePositive() {
        Smile smile = new Smile();
        smile.setSmileId(1);
        smile.setRpId("RP001");
        smile.setSource("Source");
        smile.setDestination("Destination");
        smile.setOccupancy(3);
        entityManager.persist(smile);

        smileRepository.delete(smile);

        Optional<Smile> deletedSmile = smileRepository.findById(1);
        assertFalse(deletedSmile.isPresent());
    }

    // Add more test methods as needed
}
```

This test class now includes all the requested test methods. Let me know if you need further assistance!


















Sure, here's the updated test class for the RideInfo entity:

```java
package com.cognizant.test;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.TestEntityManager;

import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;

@DataJpaTest
public class TestRideInfo {

    @Autowired
    private RideInfoRepository rideInfoRepository;

    @Autowired
    private TestEntityManager entityManager;

    @Test
    public void testFindAllPositive() {
        RideInfo rideInfo = new RideInfo();
        rideInfo.setVechileNo("ABC123");
        rideInfo.setRpId("RP001");
        rideInfo.setCarType("SUV");
        rideInfo.setCarName("Toyota RAV4");
        rideInfo.setFuelType("Petrol");
        rideInfo.setNoOfSeats(5);
        entityManager.persist(rideInfo);

        Iterable<RideInfo> it = rideInfoRepository.findAll();
        assertTrue(it.iterator().hasNext());
    }

    @Test
    public void testFindAllNegative() {
        Iterable<RideInfo> it = rideInfoRepository.findAll();
        assertFalse(it.iterator().hasNext());
    }

    @Test
    public void testFindByVechileNoPositive() {
        RideInfo rideInfo = new RideInfo();
        rideInfo.setVechileNo("ABC123");
        rideInfo.setRpId("RP001");
        rideInfo.setCarType("SUV");
        rideInfo.setCarName("Toyota RAV4");
        rideInfo.setFuelType("Petrol");
        rideInfo.setNoOfSeats(5);
        entityManager.persist(rideInfo);

        Optional<RideInfo> foundRideInfo = rideInfoRepository.findByVechileNo("ABC123");
        assertTrue(foundRideInfo.isPresent());
    }

    @Test
    public void testFindByVechileNoNegative() {
        Optional<RideInfo> notFoundRideInfo = rideInfoRepository.findByVechileNo("InvalidVechileNo");
        assertFalse(notFoundRideInfo.isPresent());
    }

    @Test
    public void testSavePositive() {
        RideInfo rideInfo = new RideInfo();
        rideInfo.setVechileNo("ABC123");
        rideInfo.setRpId("RP001");
        rideInfo.setCarType("SUV");
        rideInfo.setCarName("Toyota RAV4");
        rideInfo.setFuelType("Petrol");
        rideInfo.setNoOfSeats(5);
        rideInfoRepository.save(rideInfo);

        Optional<RideInfo> savedRideInfo = rideInfoRepository.findByVechileNo("ABC123");
        assertTrue(savedRideInfo.isPresent());
    }

    @Test
    public void testDeletePositive() {
        RideInfo rideInfo = new RideInfo();
        rideInfo.setVechileNo("ABC123");
        rideInfo.setRpId("RP001");
        rideInfo.setCarType("SUV");
        rideInfo.setCarName("Toyota RAV4");
        rideInfo.setFuelType("Petrol");
        rideInfo.setNoOfSeats(5);
        entityManager.persist(rideInfo);

        rideInfoRepository.delete(rideInfo);

        Optional<RideInfo> deletedRideInfo = rideInfoRepository.findByVechileNo("ABC123");
        assertFalse(deletedRideInfo.isPresent());
    }
}
```

This test class covers positive and negative scenarios for finding, saving, and deleting RideInfo entities. Let me know if you need further assistance!












Thank you for providing the additional entity details and correcting the data type for DL no. Here's the updated test class with the new entity attributes:

```java
package com.cognizant.test;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.TestEntityManager;

import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;

@DataJpaTest
public class RideProvideTest {

    @Autowired
    private RideProvideRepository rideProvideRepository;

    @Autowired
    private TestEntityManager entityManager;

    @Test
    public void testFindAllPositive() {
        RideProvide rideProvide = new RideProvide();
        rideProvide.setRpId("RP001");
        rideProvide.setFirstName("John");
        rideProvide.setLastName("Doe");
        rideProvide.setEmailId("john@example.com");
        rideProvide.setAdharCard(123456789012L); // Adjusted to fit within long data type
        rideProvide.setPhone(1234567890); // Adjusted to fit within int data type
        rideProvide.setDlNo("DL12345678901234");
        rideProvide.setValidUpto(LocalDate.now().plusDays(31)); // Valid upto 30 days from current date
        rideProvide.setStatus("Registered");
        entityManager.persist(rideProvide);

        Iterable<RideProvide> it = rideProvideRepository.findAll();
        assertTrue(it.iterator().hasNext());
    }

    @Test
    public void testFindAllNegative() {
        Iterable<RideProvide> it = rideProvideRepository.findAll();
        assertFalse(it.iterator().hasNext());
    }

    @Test
    public void testFindByIdPositive() {
        RideProvide rideProvide = new RideProvide();
        rideProvide.setRpId("RP001");
        rideProvide.setFirstName("John");
        rideProvide.setLastName("Doe");
        rideProvide.setEmailId("john@example.com");
        rideProvide.setAdharCard(123456789012L); // Adjusted to fit within long data type
        rideProvide.setPhone(1234567890); // Adjusted to fit within int data type
        rideProvide.setDlNo("DL12345678901234");
        rideProvide.setValidUpto(LocalDate.now().plusDays(31)); // Valid upto 30 days from current date
        rideProvide.setStatus("Registered");
        entityManager.persist(rideProvide);

        Optional<RideProvide> foundRideProvide = rideProvideRepository.findById("RP001");
        assertTrue(foundRideProvide.isPresent());
    }

    @Test
    public void testFindByIdNegative() {
        Optional<RideProvide> notFoundRideProvide = rideProvideRepository.findById("InvalidRpId");
        assertFalse(notFoundRideProvide.isPresent());
    }

    @Test
    public void testSavePositive() {
        RideProvide rideProvide = new RideProvide();
        rideProvide.setRpId("RP001");
        rideProvide.setFirstName("John");
        rideProvide.setLastName("Doe");
        rideProvide.setEmailId("john@example.com");
        rideProvide.setAdharCard(123456789012L); // Adjusted to fit within long data type
        rideProvide.setPhone(1234567890); // Adjusted to fit within int data type
        rideProvide.setDlNo("DL12345678901234");
        rideProvide.setValidUpto(LocalDate.now().plusDays(31)); // Valid upto 30 days from current date
        rideProvide.setStatus("Registered");
        rideProvideRepository.save(rideProvide);

        Optional<RideProvide> savedRideProvide = rideProvideRepository.findById("RP001");
        assertTrue(savedRideProvide.isPresent());
    }

    @Test
    public void testDeletePositive() {
        RideProvide rideProvide = new RideProvide();
        rideProvide.setRpId("RP001");
        rideProvide.setFirstName("John");
        rideProvide.setLastName("Doe");
        rideProvide.setEmailId("john@example.com");
        rideProvide.setAdharCard(123456789012L); // Adjusted to fit within long data type
        rideProvide.setPhone(1234567890); // Adjusted to fit within int data type
        rideProvide.setDlNo("DL12345678901234");
        rideProvide.setValidUpto(LocalDate.now().plusDays(31)); // Valid upto 30 days from current date
        rideProvide.setStatus("Registered");
        entityManager.persist(rideProvide);

        rideProvideRepository.delete(rideProvide);

        Optional<RideProvide> deletedRideProvide = rideProvideRepository.findById("RP001");
        assertFalse(deletedRideProvide.isPresent());
    }
}
```

I've adjusted the Adhar Card and Phone numbers to fit within the `long` and `int` data types, respectively. Additionally, I've added assertions as needed to cover more test cases.





```java
package com.cognizant.test;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.TestEntityManager;

import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;

@DataJpaTest
public class RideProvideTest {

    @Autowired
    private RideProvideRepository rideProvideRepository;

    @Autowired
    private TestEntityManager entityManager;

    @Test
    public void testFindAllPositive() {
        RideProvide rideProvide = new RideProvide();
        rideProvide.setRpId("RP001");
        rideProvide.setFirstName("John");
        rideProvide.setLastName("Doe");
        rideProvide.setEmailId("john@example.com");
        rideProvide.setDlNo("DL12345678901234");
        entityManager.persist(rideProvide);

        Iterable<RideProvide> it = rideProvideRepository.findAll();
        assertTrue(it.iterator().hasNext());
    }

    @Test
    public void testFindAllNegative() {
        Iterable<RideProvide> it = rideProvideRepository.findAll();
        assertTrue(it.iterator().hasNext());
    }

    @Test
    public void testFindByIdPositive() {
        RideProvide rideProvide = new RideProvide();
        rideProvide.setRpId("RP001");
        rideProvide.setFirstName("John");
        rideProvide.setLastName("Doe");
        rideProvide.setEmailId("john@example.com");
        rideProvide.setDlNo("DL12345678901234");
        entityManager.persist(rideProvide);

        Optional<RideProvide> foundRideProvide = rideProvideRepository.findById("RP001");
        assertTrue(foundRideProvide.isPresent());
    }

    @Test
    public void testFindByIdNegative() {
        Optional<RideProvide> notFoundRideProvide = rideProvideRepository.findById("InvalidRpId");
        assertFalse(notFoundRideProvide.isPresent());
    }

    @Test
    public void testSavePositive() {
        RideProvide rideProvide = new RideProvide();
        rideProvide.setRpId("RP001");
        rideProvide.setFirstName("John");
        rideProvide.setLastName("Doe");
        rideProvide.setEmailId("john@example.com");
        rideProvide.setDlNo("DL12345678901234");
        rideProvideRepository.save(rideProvide);

        Optional<RideProvide> savedRideProvide = rideProvideRepository.findById("RP001");
        assertTrue(savedRideProvide.isPresent());
    }

    @Test
    public void testDeletePositive() {
        RideProvide rideProvide = new RideProvide();
        rideProvide.setRpId("RP001");
        rideProvide.setFirstName("John");
        rideProvide.setLastName("Doe");
        rideProvide.setEmailId("john@example.com");
        rideProvide.setDlNo("DL12345678901234");
        entityManager.persist(rideProvide);

        rideProvideRepository.delete(rideProvide);

        Optional<RideProvide> deletedRideProvide = rideProvideRepository.findById("RP001");
        assertFalse(deletedRideProvide.isPresent());
    }
}
```
















Certainly! Below is an example of a test class for the `RideProvide` entity using JUnit and Mockito. This test class covers positive, negative, and exception scenarios for various methods in the `RideProvideService`.

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit.jupiter.SpringExtension;

import java.time.LocalDate;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)
@SpringBootTest
public class RideProvideTest {

    @Mock
    private RideProvideRepository rideProvideRepository;

    @InjectMocks
    private RideProvideService rideProvideService;

    private RideProvide rideProvide;

    @BeforeEach
    public void setUp() {
        rideProvide = new RideProvide();
        rideProvide.setRpId("RP001");
        rideProvide.setAdharCard("123456789012");
        rideProvide.setEmailId("john@example.com");
        rideProvide.setPhone(1234567890);
        rideProvide.setFirstName("John");
        rideProvide.setLastName("Doe");
        rideProvide.setDlNo("DL12345678901234");
        rideProvide.setValidUpto(LocalDate.of(2024, 12, 31));
        rideProvide.setStatus("Registered");
    }

    @Test
    public void testSaveRideProvide_Positive() {
        when(rideProvideRepository.save(rideProvide)).thenReturn(rideProvide);
        RideProvide savedRideProvide = rideProvideService.saveRideProvide(rideProvide);
        assertEquals(rideProvide, savedRideProvide);
    }

    @Test
    public void testSaveRideProvide_Negative() {
        RideProvide invalidRideProvide = new RideProvide();
        // Set invalid data or null fields in invalidRideProvide
        assertThrows(Exception.class, () -> rideProvideService.saveRideProvide(invalidRideProvide));
    }

    @Test
    public void testSaveRideProvide_Exception() {
        when(rideProvideRepository.save(rideProvide)).thenThrow(new RuntimeException("Failed to save ride provide"));
        assertThrows(RuntimeException.class, () -> rideProvideService.saveRideProvide(rideProvide));
    }

    @Test
    public void testGetRideProvideById_Positive() {
        when(rideProvideRepository.findById("RP001")).thenReturn(java.util.Optional.ofNullable(rideProvide));
        RideProvide foundRideProvide = rideProvideService.getRideProvideById("RP001");
        assertEquals(rideProvide, foundRideProvide);
    }

    @Test
    public void testGetRideProvideById_Negative() {
        when(rideProvideRepository.findById("RP002")).thenReturn(java.util.Optional.empty());
        RideProvide notFoundRideProvide = rideProvideService.getRideProvideById("RP002");
        assertNull(notFoundRideProvide);
    }

    // Add more test methods as needed
}
```

In this test class:

- `setUp`: This method initializes a `RideProvide` object with sample data before each test method.
- `testSaveRideProvide_Positive`: Tests the positive case of saving a `RideProvide` object and asserts that the saved object is equal to the original object.
- `testSaveRideProvide_Negative`: Tests the negative case of saving an invalid `RideProvide` object and expects an exception to be thrown.
- `testSaveRideProvide_Exception`: Tests the case where an exception occurs while saving a `RideProvide` object and expects a `RuntimeException` to be thrown.
- `testGetRideProvideById_Positive`: Tests the positive case of retrieving a `RideProvide` object by its ID and asserts that the retrieved object is equal to the original object.
- `testGetRideProvideById_Negative`: Tests the negative case of retrieving a `RideProvide` object by an invalid ID and asserts that no object is found.

You can add more test methods to cover additional scenarios based on your application requirements. Let me know if you need further assistance!






```sql
-- Schema for RideProvide table
CREATE TABLE RideProvide (
    Rp_Id VARCHAR(6) PRIMARY KEY,
    Adhar_Card VARCHAR(12) NOT NULL,
    Email_Id VARCHAR(255) NOT NULL,
    Phone INT NOT NULL,
    First_Name VARCHAR(255) NOT NULL,
    Last_Name VARCHAR(255) NOT NULL,
    Dl_No VARCHAR(16) NOT NULL,
    Valid_Upto DATE NOT NULL,
    Status VARCHAR(255) NOT NULL
);

-- Schema for RideInfo table
CREATE TABLE RideInfo (
    Ride_Id VARCHAR(255) PRIMARY KEY,
    Rp_Id VARCHAR(6),
    Car_Type VARCHAR(255),
    Car_Name VARCHAR(255),
    Fuel_Type VARCHAR(255),
    No_Of_Seats INT NOT NULL,
    FOREIGN KEY (Rp_Id) REFERENCES RideProvide(Rp_Id)
);

-- Schema for Simles table
CREATE TABLE Simles (
    Simles_Id VARCHAR(255) PRIMARY KEY,
    Rp_Id VARCHAR(6),
    Destination VARCHAR(255),
    Occupancy INT,
    FOREIGN KEY (Rp_Id) REFERENCES RideProvide(Rp_Id)
);
```




Apologies for the misunderstanding. Here are the schemas for the `RideProvide`, `RideInfo`, and `Smiles` tables together:

```sql
-- Insert data into RideProvide table
INSERT INTO RideProvide (Rp_Id, Adhar_Card, Email_Id, Phone, First_Name, Last_Name, Dl_No, Valid_Upto, Status)
VALUES 
('RPDO90', '123456789012', 'john@example.com', 1234567890, 'John', 'Doe', 'DL12345678901234', '2024-12-31', 'Registered'),
('RPST85', '987654321098', 'jane@example.com', 9876543210, 'Jane', 'Smith', 'DL98765432109876', '2025-01-15', 'Un-registered');

-- Insert data into RideInfo table
INSERT INTO RideInfo (Ride_Id, Rp_Id, Car_Type, Car_Name, Fuel_Type, No_Of_Seats)
VALUES 
('RID123', 'RPDO90', 'SUV', 'Toyota RAV4', 'Petrol', 5),
('RID456', 'RPST85', 'Sedan', 'Honda Civic', 'Diesel', 4);

-- Insert data into Simles table
INSERT INTO Simles (Simles_Id, Rp_Id, Destination, Occupancy)
VALUES 
('SIM001', 'RPDO90', 'Beach', 2),
('SIM002', 'RPST85', 'Mountain', 3);
```





```sql
INSERT INTO RideProvide (Adhar_Card, Email_Id, Phone, First_Name, Last_Name, Dl_No, Valid_Upto, Status)
VALUES 
('123456789012', 'john@example.com', 1234567890, 'John', 'Doe', 'DL12345678901234', '2024-12-31', 'Registered'),
('987654321098', 'jane@example.com', 9876543210, 'Jane', 'Smith', 'DL98765432109876', '2025-01-15', 'Un-registered');

INSERT INTO RideInfo (Ride_Id, Rp_Id, Car_Type, Car_Name, Fuel_Type, No_Of_Seats)
VALUES 
('RID123', 1, 'SUV', 'Toyota RAV4', 'Petrol', 5),
('RID456', 2, 'Sedan', 'Honda Civic', 'Diesel', 4);

INSERT INTO Simles (Simles_Id, Rp_Id, Destination, Occupancy)
VALUES 
('SIM001', 1, 'Beach', 2),
('SIM002', 2, 'Mountain', 3);
```




```sql
CREATE TABLE RideProvide (
    Rp_Id INT PRIMARY KEY AUTO_INCREMENT,
    Adharcard VARCHAR(12) NOT NULL,
    Emailld VARCHAR(255) NOT NULL,
    Phone INT NOT NULL,
    FirstName VARCHAR(255) NOT NULL,
    LastName VARCHAR(255) NOT NULL,
    Dl_No VARCHAR(16) NOT NULL,
    Valid_Upto DATE NOT NULL,
    Status VARCHAR(255) NOT NULL
);

CREATE TABLE RideInfo (
    Ride_Id VARCHAR(255),
    Rp_Id INT,
    Car_Type VARCHAR(255),
    Source VARCHAR(255),
    Car_Name VARCHAR(255),
    Destination VARCHAR(255),
    Fuel_Type VARCHAR(255),
    Occupancy INT NOT NULL,
    No_Of_Seats INT NOT NULL
);

CREATE TABLE Simles (
    Simles_Id VARCHAR(255),
    Rp_Id INT,
    Source VARCHAR(255),
    Destination VARCHAR(255),
    Occupancy INT
);
```

This script defines the schemas for the three tables in the specified order: `RideProvide`, `RideInfo`, and `Simles`. Let me know if you need any further assistance!




Sure, here's the `schema.sql` without the "IF NOT EXISTS" clause:

```sql
CREATE TABLE rideProvide (
    rpld INT,
    adharcard VARCHAR(255) NOT NULL,
    emailld VARCHAR(255) NOT NULL,
    phone INT NOT NULL,
    firstName VARCHAR(255) NOT NULL,
    lastName VARCHAR(255) NOT NULL,
    dlNo VARCHAR(255) NOT NULL,
    validUpto DATE NOT NULL,
    status VARCHAR(255) NOT NULL
);
```

This script creates the `rideProvide` table with the specified columns and constraints in an H2 in-memory database, without checking for existence. Let me know if you need further assistance!



CREATE TABLE rideProvide (
    rpld INT,
    adharcard VARCHAR(255) NOT NULL,
    emailld VARCHAR(255) NOT NULL,
    phone INT NOT NULL,
    firstName VARCHAR(255) NOT NULL,
    lastName VARCHAR(255) NOT NULL,
    dlNo VARCHAR(255) NOT NULL,
    validUpto DATE NOT NULL,
    status VARCHAR(255) NOT NULL
);






To incorporate the DTO classes into the `RideProvider` entity class, you would create fields for each DTO class and annotate them accordingly. Here's how you can do it:

```java
import lombok.Data;
import org.hibernate.annotations.GenericGenerator;

import javax.persistence.*;
import javax.validation.constraints.*;
import java.time.LocalDate;

@Entity
@Table(name = "rideProvider")
@Data
public class RideProvider {

    @Id
    @GeneratedValue(generator = "rideProviderIdGenerator")
    @GenericGenerator(name = "rideProviderIdGenerator", strategy = "com.cognizant.entities.RideProviderIdGenerator")
    private String rideProviderId;

    @NotNull
    @Size(min = 12, max = 12, message = "Aadhar number must be 12 digits long")
    private String adharcard;

    @NotNull
    @Email
    @Pattern(regexp = "^.*@cognizant.com$", message = "Email address should always have @cognizant.com")
    private String emailld;

    @NotNull
    @Size(min = 10, max = 10, message = "Phone number should be exactly 10 digits long")
    private String phone;

    @NotNull
    @Pattern(regexp = "^[A-Za-z]*$", message = "First name should only have alphabets")
    @Size(min = 3, message = "First name must be at least 3 characters long")
    private String firstName;

    @NotNull
    @Pattern(regexp = "^[A-Za-z]*$", message = "Last name should only have alphabets")
    @Size(min = 3, message = "Last name must be at least 3 characters long")
    private String lastName;

    @NotNull
    @Size(min = 16, max = 16, message = "Driving Licence Number must be 16 characters long")
    @Pattern(regexp = "^\\w{3}-\\w{3}-\\w{3}-\\w{3}$", message = "Invalid driving license number format")
    private String dINo;

    @NotNull
    @Future
    private LocalDate validUpto;

    @NotNull
    @Pattern(regexp = "^(Registered|Un-registered)$", message = "Status must be either 'Registered' or 'Un-registered'")
    private String status;
    
    // Include DTO fields
    
    @NotNull
    private EmailDTO emailDTO;
    
    @NotNull
    private ValidUptoDTO validUptoDTO;
    
    @NotNull
    private StatusDTO statusDTO;
    
    @NotNull
    private DrivingLicenseDTO drivingLicenseDTO;
}
```

By adding these fields, you are including the DTO classes into your `RideProvider` entity class. Ensure you have appropriate getter and setter methods for these fields in the `RideProvider` class. Adjust the annotations and constraints based on your specific requirements.
