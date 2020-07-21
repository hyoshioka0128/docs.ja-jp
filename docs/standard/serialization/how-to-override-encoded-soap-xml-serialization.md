---
title: '方法: SOAP エンコード済み XML シリアル化をオーバーライドする'
description: SOAP メッセージとしてオブジェクトの XML シリアル化をオーバーライドする方法について説明します。これは、標準の XML シリアル化をオーバーライドするプロセスに似ています。
ms.date: 03/30/2017
helpviewer_keywords:
- overriding XML serialization
- SOAP, overriding encoded XML serialization
ms.assetid: d0791df8-04e3-46b4-a6be-fe0ed09267e8
ms.openlocfilehash: 50688cb25294f14a9dd4596258eb95adf93cdb41
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84277987"
---
# <a name="how-to-override-encoded-soap-xml-serialization"></a>方法: SOAP エンコード済み XML シリアル化をオーバーライドする

SOAP メッセージとしてオブジェクトの XML シリアル化をオーバーライドするプロセスは、標準の XML シリアル化をオーバーライドするプロセスに似ています。 標準の XML シリアル化をオーバーライドする方法については、「[方法: XML ストリームの代替要素名を指定する](how-to-specify-an-alternate-element-name-for-an-xml-stream.md)」を参照してください。

## <a name="to-override-serialization-of-objects-as-soap-messages"></a>SOAP メッセージとしてオブジェクトのシリアル化をオーバーライドするには

1. <xref:System.Xml.Serialization.SoapAttributeOverrides> クラスのインスタンスを作成します。

2. シリアル化するクラス メンバーごとに `SoapAttributes` を作成します。

3. シリアル化するメンバーに対し、XML シリアル化に影響を与える 1 つ以上の属性のインスタンスを必要に応じて作成します。 詳細については、「エンコード済み SOAP シリアル化を制御する属性」を参照してください。

4. 手順 3 で作成した属性に、`SoapAttributes` の適切なプロパティを設定します。

5. `SoapAttributes` に `SoapAttributeOverrides` を追加します。

6. `XmlTypeMapping` を使用して `SoapAttributeOverrides` を作成します。 `SoapReflectionImporter.ImportTypeMapping` メソッドを使用します。

7. `XmlSerializer` を使用して `XmlTypeMapping` を作成します。

8. オブジェクトをシリアル化または逆シリアル化します。

## <a name="example"></a>例

ファイルを 2 つの方法でシリアル化するコード例を次に示します。最初の方法では `XmlSerializer` クラスの動作をオーバーライドせずにシリアル化し、2 番目の方法ではこのクラスの動作をオーバーライドしてシリアル化します。 この例には、複数のメンバーを持つ `Group` という名前のクラスが含まれています。 クラス メンバーには、`SoapElementAttribute` などのさまざまな属性が適用されています。 `SerializeOriginal` メソッドでこのクラスをシリアル化すると、これらの属性によって SOAP メッセージの内容が制御されます。 この `SerializeOverride` メソッドを呼び出すと、さまざまな属性を作成し、それらの属性に `XmlSerializer` のプロパティを設定することによって、`SoapAttributes` の動作がオーバーライドされます。

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.Serialization;
using System.Xml.Schema;

public class Group
{
    [SoapAttribute (Namespace = "http://www.cpandl.com")]
    public string GroupName;

    [SoapAttribute(DataType = "base64Binary")]
    public Byte [] GroupNumber;

    [SoapAttribute(DataType = "date", AttributeName = "CreationDate")]
    public DateTime Today;
    [SoapElement(DataType = "nonNegativeInteger", ElementName = "PosInt")]
    public string PositiveInt;
    // This is ignored when serialized unless it is overridden.
    [SoapIgnore]
    public bool IgnoreThis;

    public GroupType Grouptype;

    [SoapInclude(typeof(Car))]
    public Vehicle myCar(string licNumber)
    {
        Vehicle v;
        if(licNumber == "")
            {
                v = new Car();
            v.licenseNumber = "!!!!!!";
        }
        else
        {
            v = new Car();
            v.licenseNumber = licNumber;
        }
        return v;
    }
}

public abstract class Vehicle
{
    public string licenseNumber;
    public DateTime makeDate;
}

public class Car: Vehicle
{
}

public enum GroupType
{
    // These enums can be overridden.
    small,
    large
}

public class Run
{
    public static void Main()
    {
        Run test = new Run();
        test.SerializeOriginal("SoapOriginal.xml");
        test.SerializeOverride("SoapOverrides.xml");
        test.DeserializeOriginal("SoapOriginal.xml");
        test.DeserializeOverride("SoapOverrides.xml");

    }
    public void SerializeOriginal(string filename)
    {
        // Creates an instance of the XmlSerializer class.
        XmlTypeMapping myMapping =
        (new SoapReflectionImporter().ImportTypeMapping(
        typeof(Group)));
        XmlSerializer mySerializer =
        new XmlSerializer(myMapping);

        // Writing the file requires a TextWriter.
        TextWriter writer = new StreamWriter(filename);

        // Creates an instance of the class that will be serialized.
        Group myGroup = new Group();

        // Sets the object properties.
        myGroup.GroupName = ".NET";

        Byte [] hexByte = new Byte[2]{Convert.ToByte(100),
        Convert.ToByte(50)};
        myGroup.GroupNumber = hexByte;

        DateTime myDate = new DateTime(2002,5,2);
        myGroup.Today = myDate;

        myGroup.PositiveInt= "10000";
        myGroup.IgnoreThis=true;
        myGroup.Grouptype= GroupType.small;
        Car thisCar =(Car)  myGroup.myCar("1234566");

        // Prints the license number just to prove the car was created.
        Console.WriteLine("License#: " + thisCar.licenseNumber + "\n");

        // Serializes the class and closes the TextWriter.
        mySerializer.Serialize(writer, myGroup);
        writer.Close();
    }

    public void SerializeOverride(string filename)
    {
        // Creates an instance of the XmlSerializer class
        // that overrides the serialization.
        XmlSerializer overRideSerializer = CreateOverrideSerializer();

        // Writing the file requires a TextWriter.
        TextWriter writer = new StreamWriter(filename);

        // Creates an instance of the class that will be serialized.
        Group myGroup = new Group();

        // Sets the object properties.
        myGroup.GroupName = ".NET";

        Byte [] hexByte = new Byte[2]{Convert.ToByte(100),
        Convert.ToByte(50)};
        myGroup.GroupNumber = hexByte;

        DateTime myDate = new DateTime(2002,5,2);
        myGroup.Today = myDate;

        myGroup.PositiveInt= "10000";
        myGroup.IgnoreThis=true;
        myGroup.Grouptype= GroupType.small;
        Car thisCar =(Car)  myGroup.myCar("1234566");

        // Serializes the class and closes the TextWriter.
        overRideSerializer.Serialize(writer, myGroup);
         writer.Close();
    }

    public void DeserializeOriginal(string filename)
    {
        // Creates an instance of the XmlSerializer class.
        XmlTypeMapping myMapping =
        (new SoapReflectionImporter().ImportTypeMapping(
        typeof(Group)));
        XmlSerializer mySerializer =
        new XmlSerializer(myMapping);

        TextReader reader = new StreamReader(filename);

        // Deserializes and casts the object.
        Group myGroup;
        myGroup = (Group) mySerializer.Deserialize(reader);

        Console.WriteLine(myGroup.GroupName);
        Console.WriteLine(myGroup.GroupNumber[0]);
        Console.WriteLine(myGroup.GroupNumber[1]);
        Console.WriteLine(myGroup.Today);
        Console.WriteLine(myGroup.PositiveInt);
        Console.WriteLine(myGroup.IgnoreThis);
        Console.WriteLine();
    }

    public void DeserializeOverride(string filename)
    {
        // Creates an instance of the XmlSerializer class.
        XmlSerializer overRideSerializer = CreateOverrideSerializer();
        // Reading the file requires a TextReader.
        TextReader reader = new StreamReader(filename);

        // Deserializes and casts the object.
        Group myGroup;
        myGroup = (Group) overRideSerializer.Deserialize(reader);

        Console.WriteLine(myGroup.GroupName);
        Console.WriteLine(myGroup.GroupNumber[0]);
        Console.WriteLine(myGroup.GroupNumber[1]);
        Console.WriteLine(myGroup.Today);
        Console.WriteLine(myGroup.PositiveInt);
        Console.WriteLine(myGroup.IgnoreThis);
    }

    private XmlSerializer CreateOverrideSerializer()
    {
        SoapAttributeOverrides mySoapAttributeOverrides =
        new SoapAttributeOverrides();
        SoapAttributes soapAtts = new SoapAttributes();

        SoapElementAttribute mySoapElement = new SoapElementAttribute();
        mySoapElement.ElementName = "xxxx";
        soapAtts.SoapElement = mySoapElement;
        mySoapAttributeOverrides.Add(typeof(Group), "PositiveInt",
        soapAtts);

        // Overrides the IgnoreThis property.
        SoapIgnoreAttribute myIgnore = new SoapIgnoreAttribute();
        soapAtts = new SoapAttributes();
        soapAtts.SoapIgnore = false;
        mySoapAttributeOverrides.Add(typeof(Group), "IgnoreThis",
        soapAtts);

        // Overrides the GroupType enumeration.
        soapAtts = new SoapAttributes();
        SoapEnumAttribute xSoapEnum = new SoapEnumAttribute();
        xSoapEnum.Name = "Over1000";
        soapAtts.SoapEnum = xSoapEnum;

        // Adds the SoapAttributes to the
        // mySoapAttributeOverrides.
        mySoapAttributeOverrides.Add(typeof(GroupType), "large",
        soapAtts);

        // Creates a second enumeration and adds it.
        soapAtts = new SoapAttributes();
        xSoapEnum = new SoapEnumAttribute();
        xSoapEnum.Name = "ZeroTo1000";
        soapAtts.SoapEnum = xSoapEnum;
        mySoapAttributeOverrides.Add(typeof(GroupType), "small",
        soapAtts);

        // Overrides the Group type.
        soapAtts = new SoapAttributes();
        SoapTypeAttribute soapType = new SoapTypeAttribute();
        soapType.TypeName = "Team";
        soapAtts.SoapType = soapType;
        mySoapAttributeOverrides.Add(typeof(Group),soapAtts);

        // Creates an XmlTypeMapping that is used to create an instance
        // of the XmlSerializer class. Then returns the XmlSerializer.
        XmlTypeMapping myMapping = (new SoapReflectionImporter(
        mySoapAttributeOverrides)).ImportTypeMapping(typeof(Group));

        XmlSerializer ser = new XmlSerializer(myMapping);
        return ser;
    }
}
```

## <a name="see-also"></a>関連項目

- [XML シリアル化および SOAP シリアル化](xml-and-soap-serialization.md)
- [エンコード済み SOAP シリアル化を制御する属性](attributes-that-control-encoded-soap-serialization.md)
- [XML Web サービスを使用した XML シリアル化](xml-serialization-with-xml-web-services.md)
- [方法: オブジェクトをシリアル化する](how-to-serialize-an-object.md)
- [方法: オブジェクトを逆シリアル化する](how-to-deserialize-an-object.md)
- [方法: オブジェクトを SOAP エンコード済み XML ストリームとしてシリアル化する](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
