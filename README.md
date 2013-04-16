OC Mapper for Objective C
=========================

OCMapper is an NSDictionary to NSObject convertor.

Features:
- Supports array structures
- Supports Tree Structures
- Supports complex object nesting 
- Auto detects key/values based on NSDictionary keys
- Fully Configurable
- Does not require subclassing or adding any extra code to your model
- Convert Date values to NSDate
- Takes default dateformatter and uses it for all NSDate conversions
- NSDate conversion can be configured based on specific class & properties

Let's say these are our models
```objective-c
@interface User
@property (nonatomic, strong) NSString *firstName;
@property (nonatomic, strong) NSString *lastName;
@property (nonatomic, strong) NSNumber *age;
@property (nonatomic, strong) NSDate *dateOfBirth;
@property (nonatomic, strong) Address *address;
@property (nonatomic, strong) Post *Posts;
@end

@interface Address
@property (nonatomic, strong) NSString *city;
@property (nonatomic, strong) NSString *country;
@end

@interface Post
@property (nonatomic, strong) NSString *title;
@property (nonatomic, strong) User *author;
@end
```

Simple Automatic Mapping
-------------------------
Simple mapping when all dictionary key/values match the property names
```objective-c
{
   "firstName"   : "Aryan"
   "lastName"    : "Ghassemi"
   "age"         : 26
   "dateOfBirth" : "01/01/2013"
}

User *user = [User objectFromDictionary:aDictionary];
```

Simple Custom Mapping
-------------------------
Simple mapping when all dictionary key/values match the property names
keys for lastname and dateOfBirth don't match
```objective-c
{
   "firstName"   : "Aryan"
   "surName"    : "Ghassemi"
   "age"         : 26
   "dob" : "01/01/2013"
}

[[ObjectMapper sharedInstance] mapFromDictionaryKey:@"surName" toPropertyKey:@"lastName" forClass:[NSString class]];
[[ObjectMapper sharedInstance] mapFromDictionaryKey:@"dob" toPropertyKey:@"dateOfBirth" forClass:[NSString class]];
User *user = [User objectFromDictionary:aDictionary];
```
