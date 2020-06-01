## Fn::FindInMap
## Accessing Mapping Values

- We use Fn::FindInMap to return a named value from a specific key.
- !FindInMap [MapName, TopLevelKey, SecondLevelKey]

example for following mapping: 

```

Mappings:
  AWSRegionArch2AMI:
    us-east-1:
      HVM64: ami-6869aa05
    us-west-2:
      HVM64: ami-7172b611
    us-west-1:
      HVM64: ami-31490d51

```

we can refer as: 
```
ImageId: !FindInMap [AWSRegionArch2AMI, !Ref 'AWS::Region', HVM64]
```


---

## Pseudo Parameters Reference: 

you might have noticed that in some templates, we have some values/variables as : 
```
'AWS::Region'
in
ImageId: !FindInMap [AWSRegionArch2AMI, !Ref 'AWS::Region', HVM64]
```

this looks like a string in yaml. buy yaml does not have string with '' or "". 
these are pseudo parameters which are provided by aws and can be used in cloud formation templates. 

few types are: 
- AWS::AccountId
- AWS::NotificationARNs
- AWS::NoValue
- AWS::Region
- AWS::StackId
- AWS::StackName

Reference: 
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/pseudo-parameter-reference.html 

---

