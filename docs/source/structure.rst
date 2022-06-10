Design
======

Modules:

1. Order System
2. Record System
3. Manage System

1.OrderSystem
-----------
**DataBase**::

  Rec:Order->[Staff_ID]->Rec:Staff
           ->[User_ID] ->Rec:User
  An Order:
    The Infomation need to be restored in database:
    {
      *ID
        OrderID <- Generated  {Page:[]}
        StaffID <- Rec:Staff  {Page:[]}
        StoreID <- Rec:Store  {Page:[Order]}
        UserID  <- Rec:User   {Page:[Order:SelectUser]}
        RecordID <- [NOW]:generatedID [TODO]:a page {Page:[Order]}
          /*If the ProductType is TreatMent*/
      *Info
        OrderTime <- Generated {Page:[OrderList]}
        *Person
          IsSelf {Page:[Order]}
            Name
        Price {Page:[Order,OrderList]}
        IsPayed {Page:[Order]}
        PayedWay {Page:[Order]}
          /*{"WeiXin","TimesCard","Balance","Alipay","Cash"}*/ 
          [TODO]:Generate The PayCode.
          Desc:
              
        *ProductType
          {"TimesCard","Balance","Treatment","Medicine"}
          *TimesCard
            TotalTimes
            RemainingTimes
            Price
            Desc
          *Balance
            Money
              Balance <- (func: Money->Balance)
        ProductId <- RecProduct
        Desc
     }
  An User:
    {
      *ID
        UserID {Page:[]}
      *PersonalInfo {Page:[User]}
        WeChat {Page:[AddUser]}
        Phone {Page:[AddUser,Order:SelectUser]}
        Name {Page:[AddUser,Order:SelectUser]}
        Sex {Page:[AddUser,Order:SelectUser]}
        Age {Page:[AddUser,]}
        Weight {Page:[AddUser]}
        AddTime {Page:[AddUser]}
        LastRecordTime {Page:[Order:SelectUser]} <- Generated
        Desc {Page:[User]}
      *Info {Page:[User]}
        *TimesCard {Page:[Order:SelectUser]}
          RemainingTimes
          Price {Page:[Order:Product]}
          TotalTimes {Page:[Order:Product]}
          Desc 
        *Balance {Page:[Order:SelectUser]}
          BalaceValue 
          Money {Page:[Order:Product]}
     }
  An Staff {Page:[]}
    {
      *ID
        StaffID 
      *Info
        Name
      *Skill[TODO]
      *Wage
        LatestWageID <- Rec:Wage
    }
  An Store
    {
      *ID
        StoreID
      *Info
        Name
        Location
    }
  An Wage {Page:[Wage]}
    {
      *ID
        WageID {Page:[]}
        StaffID {Page:[]}
      *Info
        Time {Page:[Wage]}
        TimeRange {Page:[Wage]}
        Value {Page:[Wage]}
        [TODO]:DetailList {Page:[Wage]}
          /*Form: [[OrderId,UserId,Time,Price,PayWay,Wage]]*/   
    }
  
**Pages**::

  [Page]OrderList
  [Page]Order
    [Module]SelectUser
      ->AddUser
      ->User
    [Module]Product
  [Page]AddUser
  [Page]User
  [Page]Wage
  
**PageLogic**::
[Page]Root
  [Module]Button:OrderList
  [Module]Button:"add order"
    ->[Page]Order
      ->[Page]AddUser
      ->[Page]User
  [Module]Button:"user"
    ->[Page]User
  [Module]Button:Wage
      
        
          
      
    
