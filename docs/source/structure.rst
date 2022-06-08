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
      ID
        OrderID <- Generated 
        StaffID <- Rec:Staff
        StoreID <- Rec:Store
        UserID  <- Rec:User
        RecordID <- [NOW]:generatedID [TODO]:a page
      Info
        OrderTime <- Generated
        *Person
          IsSelf
            Name
        Price
        IsPayed
          *PayedWay
            {"WeiXin","TimesCard","Balance","Alipay","Cash"}
            [TODO]:Generate The PayCode.
            Desc:
              
        *ProductType
          {"TimesCard","Balance","Treatment","Medicine"}
          *TimesCard
            TotalTimes
            Times
          *Balance
            Money
              Balance <- (func: Money->Balance)
        ProductId
        Desc
     }
  An User:
    {
      ID
        UserID
      PersonalInfo
        WeChat
        Phone
        Name
        Sex
        Age
        Weight
        AddTime
        LastRecordTime
        Desc
      Info
        TimesCard
          Times
          Price
          TotalTimes
        Balance
          BalaceValue
          Money
     }
  An 
   
        
          
      
    
