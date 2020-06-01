## Resources
- resources are core of your cloudformation template. 
- they represent different aws components that will be created and configured. 
- resources are declared and can reference each other. 

- aws figures out creation, updates, and deletes of resources for us.
- there are over 224 types of resources (!)

- Resouce types identifiers are of the form: 
```   
AWS::aws-product-name::data-type-name
```

- reference: 
    https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html

- eg for ec2 instacne we will use: 
    https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-instance.html 