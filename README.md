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
