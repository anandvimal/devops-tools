## What are parameters?
- Parameters are way to provide inputs to your AWS CloudFormation template.
- If some resource configure can change type in future, define it with parameters. 

- Type: 
    - String
    - Number
    - CommaDelimitedList
    - List<Type>
    - AWS Parameter (to help catch invalid values --match against existing values in AWS Account)
- Description
- Constraints
- ConstraintDescription (String)
- Min/MaxLength
- Min/MaxValue
- Defaults
- AllowedValues (array)
- AllowedPattern (regexp)
- NoEcho (Boolean)

---

## Documentation on parameters: 
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html 

---

- the Fn::Ref function can be leveraged to reference parameters. 
- Parameters can be used anywhere in a template. 
- The shorthand for this in YAML is !Ref
- The function can also reference other elements within the template. 


