# Popular Validation Rules for Salesforce Flows including Phone, Email and Address Fields

It is important to build validation rules into your flows. If you skip this step, you will end up with errors, when your users enter information that is not in compliance with the field definition or the validation rules that are built into your field.

My popular validation rules for flows are as follows.

## Name fields:

Standard length for Name Fields are 40 for First Name, 20 for Middle Name and 80 for Last Name.


```bash
LEN({!First_Name})<=40
```
## Social Security Number:
Validation rule (this rule allows for dashes as well):
```bash
OR( 

REGEX( {!Social_Security_Number} , "[0-9X\\-]{11}"), 

REGEX( {!Social_Security_Number} , "[0-9]{9}") 

) 
```
## Address fields:
Standard length for address fields are 256 for Street Address and 80 for City. The ZIP (Postal) code can be in XXXXX or in XXXXX-XXXX format.
```bash
NOT( 

 AND( 

   NOT(ISBLANK({!State})), 

   OR( 

      LEN( {!State}) <> 2, 

      NOT(CONTAINS({!State}, UPPER({!State}))) 

    ) 

 ) 

) 
```
## ZIP (Postal) Code

ZIP code needs to be in XXXXX or in XXXXX-XXXX format. 
```bash
REGEX({!MailingZIP} , “\\d{5}(-\\d{4})?”) \
```

## Revenue (Currency/Number Length):
```bash
{!Revenue}<10000000000000000
```

## Email:

```bash
REGEX({!Email_Address},”[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}”)
```
## Phone number:
```bash
AND( 

LEN({!Mobile_Phone})=10, 

NOT(REGEX({!Mobile_Phone} ,"^[a-z A-Z]*$")) 

) 
```
