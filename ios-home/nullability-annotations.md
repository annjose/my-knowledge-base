# Nullability Annotations

Two groups of nullability annotations -`_Nullable/_Nonnull` and `nullable/nonnull`. The lowercase one is more elegant and works for almost all scenarios:

* Method declarations - write the annotation right after the open parenthesis of the parameter
  * `- (nullable NSString *) getItemWithIdentifier:(nonnull NSString*)identifier;` 
* Property declarations - write the annotation in the attributes list
  * `@property (copy, nonnull) NSString* name;`
* You can also define Nullability regions to mark specific regions in the file to consider any pointer type to be nonnull. So you need to explicitly mark only `nullable` properties/parameters
  *  `NS_ASSUME_NONNULL_BEGIN` and `NS_ASSUME_NONNULL_END`

Source: [https://developer.apple.com/swift/blog/?id=25](https://developer.apple.com/swift/blog/?id=25)

