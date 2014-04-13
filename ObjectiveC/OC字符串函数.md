### strings.Split方法
分隔字符串
```
NSArray* foo = [@"10/04/2011" componentsSeparatedByString: @"/"];
```

### strings.Join方法
合并字符串
```
NSArray  *array1 = [NSArray arrayWithObjects:@"1", @"2", @"3", nil];
NSString *joinedString = [array1 componentsJoinedByString:@","];
```

### fmt.Sprintf方法
```
[NSString stringWithFormat:@"[FvzIapCFinishTransaction] transactionId[%s] not found", OCTransactionId];
```