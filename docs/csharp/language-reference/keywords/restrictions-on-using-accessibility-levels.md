---
title: アクセシビリティ レベルの使用に関する制限事項 - C# リファレンス
ms.date: 07/20/2015
helpviewer_keywords:
- access modifiers [C#], accessibility level restrictions
ms.assetid: 987e2f22-46bf-4fea-80ee-270b9cd01045
ms.openlocfilehash: 8082dbd7398b6634b68f1dd2887cd55d6798a5d9
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795158"
---
# <a name="restrictions-on-using-accessibility-levels-c-reference"></a>アクセシビリティ レベルの使用に関する制限事項 (C# リファレンス)

宣言で型を指定する場合、その型のアクセシビリティ レベルがメンバーまたは他の型のアクセシビリティ レベルに依存するかどうかをチェックしてください。 たとえば、直接基底クラスは、少なくともその派生クラスと同程度にアクセス可能である必要があります。 次の宣言はコンパイラ エラーになりますが、それは基底クラス `BaseClass` のアクセシビリティが `MyClass` のアクセシビリティよりも低いためです。

```csharp
class BaseClass {...}
public class MyClass: BaseClass {...} // Error
```

宣言されたアクセシビリティ レベルの制限を次の表にまとめます。

|コンテキスト|解説|
|-------------|-------------|
|[クラス](../../programming-guide/classes-and-structs/classes.md)|クラスの型の直接基底クラスは、少なくとも、クラスの型自体と同程度にアクセス可能である必要があります。|
|[インターフェイス](../../programming-guide/interfaces/index.md)|インターフェイスの型の明示的な基本インターフェイスは、少なくとも、インターフェイスの型自体と同程度にアクセス可能である必要があります。|
|[デリゲート](../../programming-guide/delegates/index.md)|デリゲート型の戻り値の型およびパラメーターの型は、少なくとも、デリゲート型自体と同程度にアクセス可能である必要があります。|
|[定数](../../programming-guide/classes-and-structs/constants.md)|定数の型は、少なくとも定数自体と同程度にアクセス可能である必要があります。|
|[フィールド](../../programming-guide/classes-and-structs/fields.md)|フィールドの型は、少なくともフィールド自体と同程度にアクセス可能である必要があります。|
|[メソッド](../../programming-guide/classes-and-structs/methods.md)|メソッドの戻り値の型およびパラメーターの型は、少なくとも、メソッド自体と同程度にアクセス可能である必要があります。|
|[Properties](../../programming-guide/classes-and-structs/properties.md)|プロパティの型は、少なくともプロパティ自体と同程度にアクセス可能である必要があります。|
|[イベント](../../programming-guide/events/index.md)|イベントの型は、少なくともイベント自体と同程度にアクセス可能である必要があります。|
|[インデクサー](../../programming-guide/indexers/index.md)|インデクサーの型とパラメーターの型は、少なくとも、インデクサー自体と同程度にアクセス可能である必要があります。|
|[オペレーター](../operators/index.md)|演算子の戻り値の型とパラメーターの型は、少なくとも、演算子自体と同程度にアクセス可能である必要があります。|
|[コンストラクター](../../programming-guide/classes-and-structs/constructors.md)|コンストラクターのパラメーターの型は、少なくとも、コンストラクター自体と同程度にアクセス可能である必要があります。|

## <a name="example"></a>例

さまざまな型の不適切な宣言の例を次に示します。 各宣言の後のコメントは、予期されるコンパイラ エラーを示しています。

```csharp
// Restrictions on Using Accessibility Levels
// CS0052 expected as well as CS0053, CS0056, and CS0057
// To make the program work, change access level of both class B
// and MyPrivateMethod() to public.

using System;

// A delegate:
delegate int MyDelegate();

class B
{
    // A private method:
    static int MyPrivateMethod()
    {
        return 0;
    }
}

public class A
{
    // Error: The type B is less accessible than the field A.myField.
    public B myField = new B();

    // Error: The type B is less accessible
    // than the constant A.myConst.
    public readonly B myConst = new B();

    public B MyMethod()
    {
        // Error: The type B is less accessible
        // than the method A.MyMethod.
        return new B();
    }

    // Error: The type B is less accessible than the property A.MyProp
    public B MyProp
    {
        set
        {
        }
    }

    MyDelegate d = new MyDelegate(B.MyPrivateMethod);
    // Even when B is declared public, you still get the error:
    // "The parameter B.MyPrivateMethod is not accessible due to
    // protection level."

    public static B operator +(A m1, B m2)
    {
        // Error: The type B is less accessible
        // than the operator A.operator +(A,B)
        return new B();
    }

    static void Main()
    {
        Console.Write("Compiled successfully");
    }
}
```

## <a name="c-language-specification"></a>C# 言語仕様

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>参照

- [C# リファレンス](../index.md)
- [C# プログラミングガイド](../../programming-guide/index.md)
- [C# のキーワード](index.md)
- [アクセス修飾子](access-modifiers.md)
- [アクセシビリティ ドメイン](accessibility-domain.md)
- [アクセシビリティ レベル](accessibility-levels.md)
- [アクセス修飾子](../../programming-guide/classes-and-structs/access-modifiers.md)
- [public](public.md)
- [private](private.md)
- [protected](protected.md)
- [internal](internal.md)
