Apologies for the misunderstanding. Here are the schemas for the `RideProvide`, `RideInfo`, and `Smiles` tables together:

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
