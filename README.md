UIKitSwagger
============

Extensions to UIKit for searching/manipulating view hierarchies, finding/comparing layout constraints and additional tasks related to UIKit.


### View Subscripting

Shorten the syntax for finding and altering views in a view's hierarchy.

**Subviews** (non-negative integer indices)
- `view[index]` returns `view.subviews[index]`
- `view[index]` will return nil for an out-of-bounds index instead of raising an exception
- `view[index] = otherSubview` replaces the subview at `index` with `otherSubview`
- `view[index] = nil` simply removes the subview at `index`

**Superviews** (negative integer indices)
- `view[-1]` is equivalent to `view.superview`
- `view[-2]` is equivalent to `view.superview.superview`, etc.
- `view[-1] = otherView` moves `view` from `view.superview.subviews` to `otherView.subviews` (as will any other negative value of `index`)

Not sure where to add constraints for two items?  It's always the first common ancestor!
- `func firstCommonAncestor(view: UIView) -> UIView?`

Find `exchangeSubviewAtIndex(_: Int, withSubviewAtIndex: Int)` to be too wordy?  Try `swap(Int, Int)` instead!


### View Show/Hide

A few simply functions for hiding or showing views in a single statement are provided:

- `func HideViews(UIView...)`
- `func HideViews([UIView])`
- `func ShowViews(UIView...)`
- `func ShowViews([UIView])`


## Auto Layout

> In the source code and this documentation, the following type alias is used:
`typealias Constraint = NSLayoutConstraint`

### Constraint Search

Don't clutter your view controller code trying to find a particular constraint to remove!   Finding constraints is much easier with these methods:
- `func constraintsForItem(AnyObject) -> [Constraint]?`
- `func constraintsForAttribute(NSLayoutAttribute) -> [Constraint]?`
- `func constraintsForAttributedItem(AutoLayoutAttributedItem) -> [Constraint]?`
- `func constraintsForItems(AnyObject, AnyObject) -> [Constraint]?`
- `func constraintsForItems(AutoLayoutAttributedItem, AutoLayoutAttributedItem) -> [Constraint]?`


**Reversal:**
Want to reverse the items in a constraint to produce an equivalent constraint?
`func reversed() -> Constraint?`


**Equality:**
Compare two constraints with respect to the items, attributes, relation, multiplier and constant.  It even tries the reverse of one operand to truly determine equivalency.  In addition, the `==*` operator can be used to compare constraints for extended equivalency by comparing constraint priorities and identifiers.
