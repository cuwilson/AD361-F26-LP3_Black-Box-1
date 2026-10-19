| Classification | Partition | Range or Condition | Expected Result |
|---|---|---|---|
| Number of nights | Invalid low | Fewer than 1 night | `ValueError` |
| Number of nights | Valid | 1–31 nights | Reservation accepted if all other conditions are valid |
| Number of nights | Invalid high | More than 31 nights | `ValueError` |

| Classification | Partition | Range or Condition | Expected Result |
|---|---|---|---|
| Number of guests | Invalid low | Fewer than 1 guest | `ValueError` |
| Number of guests | Valid, standard rate | 1–5 guests | No additional guest fee |
| Number of guests | Valid, additional fee | 6–12 guests | Additional $25 per guest over five, per night |
| Number of guests | Invalid high | More than 12 guests | `ValueError` |

| Classification | Partition | Range or Condition | Expected Result |
|---|---|---|---|
| Check-in and checkout dates | Invalid, same date | Check-in date equals checkout date | `ValueError` |
| Check-in and checkout dates | Valid | Check-in date is before checkout date, with a stay of 1–31 nights | Reservation accepted if all other conditions are valid |
| Check-in and checkout dates | Invalid, reversed dates | Check-in date is after checkout date | `ValueError` |
| Check-in and checkout dates | Invalid, too long | Check-out date is greater than 31 nights after check-in date | `ValueError` |

| Classification | Partition | Range or Condition | Expected Result |
|---|---|---|---|
| Availability | Valid, fully available | Every requested night is available | Reservation accepted if all other conditions are valid |
| Availability | Invalid, partially unavailable | At least one requested night is unavailable | `UnavailableError` |
| Availability | Invalid, fully unavailable | All requested nights are unavailable | `UnavailableError` |



### Step 3: Test Cases

#### A. Number of Nights

| Test-case ID | Classification | Partition | Input | Expected Result |
|---|---|---|---|---|
| TC01 | Number of nights | Invalid low | 0 nights | `ValueError` |
| TC02 | Number of nights | Valid | 1 night | Reservation accepted at $200/night plus flat $50 cleaning fee if all other conditions are valid |
| TC03 | Number of nights | Invalid high | 32 nights | `ValueError` |

#### B. Number of Guests

| Test-case ID | Classification | Partition | Input | Expected Result |
|---|---|---|---|---|
| TC04 | Number of guests | Invalid low | 0 guests | `ValueError` |
| TC05 | Number of guests | Valid, standard rate | 1 guest | No additional guest fee, $200/night plus flat $50 cleaning fee |
| TC06 | Number of guests | Valid, additional fee | 6 guests | Additional $25/night for the sixth guest, plus the regular $200/night and flat $50 cleaning fee |
| TC07 | Number of guests |Invalid high | 13 guests | `ValueError` |

#### C. Check-in/out dates

| Test-case ID | Classification | Partition | Input | Expected Result |
|---|---|---|---|---|
| TC08 | Check-in and checkout dates | Invalid, same date | Check-in: Oct 17, Check-out: Oct 17 | `ValueError` |
| TC09 | Check-in and checkout dates | Valid | Check-in: Oct 17, Check-out: Oct 18 | Reservation accepted if all other conditions are valid |
| TC10 | Check-in and checkout dates | Invalid, reversed dates | Check-in: Oct 17, Check-out: Oct 16 | `ValueError` |
| TC11 | Check-in and checkout dates | Invalid, too long | Check-in: Oct 17, Check-out: Nov 18 | `ValueError` |

#### D. Availability

**Assuming Oct 18, 19, and 20 were already booked, with checkout on Oct 21**

| Test-case ID | Classification | Partition | Input | Expected Result |
|---|---|---|---|---|
| TC12 | Availability | Valid | Check-in: Oct 16, Check-out: Oct 18 | Reservation accepted if all other conditions are valid |
| TC13 | Availability | Invalid, partially unavailable | Check-in: Oct 16, Check-out: Oct 19 | `UnavailableError` |
| TC14 | Availability | Invalid, fully unavailable | Check-in: Oct 18, Check-out: Oct 20 | `UnavailableError` |