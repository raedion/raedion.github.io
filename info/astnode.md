# ASTNode
AST(抽象構文木)の操作を行う際の各構文のノード(単位)として扱う. この時、ASTNodeはソースコードからASTParserによって読み取られた各構文要素をノード化することで得られる. 

私が研究している「自動プログラム修正」の分野では、プログラム修正対象として「式」と「文」の二つを扱っているので、それぞれのノードの説明を行う. 

### Statement(org.eclipse.jdt.core.dom) - 文
StatementはASTNodeを継承したクラスで、ASTにおける文の構文を定義している. (詳細は[こちら]([Class Statement (ibm.com)](https://www.ibm.com/support/knowledgecenter/SS8PJ7_9.5.0/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/dom/Statement.html)))
Statementには以下のものがある. 

- AssertStatement.java
- Block.java
- BreakStatement.java
- ConstructorInvocation.java
- ContinueStatement.java
- DoStatement.java
- EnhancedForStatement.java
- ExpressionStatement.java
- ForStatement.java
- ForStatement.java
- IfStatement.java
- LabeledStatement.java
- ReturnStatement.java
- SuperConstructorInvocation.java
- SwitchCase.java
- SwitchStatement.java
- SynchronizedStatement.java
- ThrowStatement.java
- TryStatement.java
- TypeDeclarationStatement.java
- VariableDeclarationStatement.java
- WhileStatement.java

一つ一つを説明するのは省略する. 詳しく知りたい方はibmの公式サイトで確認するといい. 

#### Statementの定義

ここでは、

- Statementの使い方

について述べる

| Statement                    | 構文定義                                                     |
| ---------------------------- | ------------------------------------------------------------ |
| AssertStatement              | assert **Expression** [ : **Expression** ] ;                 |
| Block                        | { {**Statement**} }                                          |
| BreakStatement               | break [ **Identifier** ] ;                                   |
| ConstructorInvocation        | [ < **Type** { , **Type** } > ]   <br />     this ( [ **Expression** { , **Expression** } ] ) ; |
| ContinueStatement            | continue [ **Identifier** ] ;                                |
| DoStatement                  | do **Statement** while ( **Expression** ) ;                  |
| EmptyStatement               | ;                                                            |
| EnhancedForStatement         | for ( FormalParameter : **Expression** )   <br />             **Statement** |
| ExpressionStatement          | **StatementExpression** ;                                    |
| ForStatement                 | for (<br />                         [ **ForInit** ];<br />                        [ **Expression** ] ;<br />                         [ **ForUpdate** ] )<br />                         **Statement**  <br />**ForInit**:<br />                 **Expression** { , **Expression** }  <br />**ForUpdate**:<br />                 **Expression** { , **Expression** } |
| IfStatement                  | if ( **Expression** ) **Statement** [ else **Statement**]    |
| LabeledStatement             | Identifier : **Statement**                                   |
| ReturnStatement              | return [ **Expression** ] ;                                  |
| SuperConstructorInvocation   | [ **Expression** . ]<br />          [ < **Type** { , **Type** } > ]<br />          super ( [ **Expression** { , **Expression** } ] ) ; |
| SwitchCase                   | case **Expression**  : <br />                default :       |
| SwitchStatement              | switch ( **Expression** )<br />                         { { **SwitchCase** \| **Statement** } } } |
| SynchronizedStatement        | synchronized ( **Expression** ) **Block**                    |
| ThrowStatement               | throw **Expression** ;                                       |
| TryStatement                 | try [ ( **Resources** ) ]<br />          **Block**<br />          [ { **CatchClause** } ]<br />          [ finally **Block** ] |
| TypeDeclarationStatement     | **TypeDeclaration**<br />**EnumDeclaration**                 |
| VariableDeclarationStatement | { **ExtendedModifier** } **Type** **VariableDeclarationFragment**<br />         { , **VariableDeclarationFragment** } ; |
| WhileStatement               | while ( **Expression** ) **Statement**                       |

##### 各種呼び出せるメソッド一覧

- AssertStatement.java
| メソッド                               | 戻り値        | 機能                                                         |
| -------------------------------------- | :------------ | :----------------------------------------------------------- |
| `getExpression()`                      | `Expression`  | Returns the first expression of this assert statement.       |
| `getMessage()`                         | `Expression`  | Returns the message expression of this assert statement, or `null` if there is none. |
| `propertyDescriptors(int apiLevel)`    | `static List` | Returns a list of structural property descriptors for this node type. |
| `setExpression(Expression expression)` | `void`        | Sets the first expression of this assert statement.          |
| `setMessage(Expression expression)`    | `void`        | Sets or clears the message expression of this assert statement. |

- Block.java
| メソッド                          | 戻り値        | 機能                                                         |
| --------------------------------- | :------------ | :----------------------------------------------------------- |
| propertyDescriptors(int apiLevel) | `static List` | Returns a list of structural property descriptors for this node type. |
| `statements()`                    | `List`        | Returns the live list of statements in this block.           |

- BreakStatement.java
- ConstructorInvocation.java
- ContinueStatement.java
- DoStatement.java
- EnhancedForStatement.java
- ExpressionStatement.java
- ForStatement.java
- ForStatement.java
- IfStatement.java
- LabeledStatement.java
- ReturnStatement.java
- SuperConstructorInvocation.java
- SwitchCase.java
- SwitchStatement.java
- SynchronizedStatement.java
- ThrowStatement.java
- TryStatement.java
- TypeDeclarationStatement.java
- VariableDeclarationStatement.java
- WhileStatement.java


### BodyDeclaration

 ASTNodeの子クラスの一つで、各種宣言は大体これを引き継いでいる. 詳しいことは[こちら](https://www.ibm.com/support/knowledgecenter/SSZHNR_1.0.0/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/dom/BodyDeclaration.html)を参照

このクラスに含まれる Modifier (修飾子) のリストを参照することにより、このクラスを引き継いでいるところでダウンキャストすれば参照可能になる.

```java
final static void X() {}	// 得られるのは List ( [final, static] ) になる
```

#### FieldDeclaration

上記BodyDeclarationを継承している. クラス内部において、フィールド変数の宣言をになっているノードである. 詳しくは[こちら](https://www.ibm.com/support/knowledgecenter/SSZHNR_1.0.0/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/dom/FieldDeclaration.html)を参照.

構文は以下のようである.

```java
[Javadoc] { ExtendedModifier } Type VariableDeclarationFragment
     { , VariableDeclarationFragment } ;
```

ExtendedModifierは継承元であるBodyDeclarationから取得する必要がある. VariableDeclationFragmentは内部メソッドである fragments() にてListとして取得可能. 

```Java
class FieldDeclaration extends BodyDeclaration { ... }
```

| メソッド                            | 戻り値        | 機能                                                         |
| ----------------------------------- | ------------- | ------------------------------------------------------------ |
| `fragments()`                       | `List`        | Returns the live list of variable declaration fragments in this field declaration. |
| `getType()`                         | `Type`        | Returns the base type declared in this field declaration.    |
| `propertyDescriptors(int apiLevel)` | `static List` | Returns a list of structural property descriptors for this node type. |
| `setType(Type type)`                | `void`        | Sets the base type declared in this field declaration to the given type. |

得られたfragmentのリストは、[VariableDeclarationFragment](https://www.ibm.com/support/knowledgecenter/ja/SSZHNR_1.0.0/org.eclipse.jdt.doc.isv-3.14.100/reference/api/org/eclipse/jdt/core/dom/VariableDeclarationFragment.html) にキャストすれば利用可能になる. キャストエラーが不安な場合は、instanceof を利用して型の確認をしておけばよいだろう. 

### 代入式

[Assignment](https://www.ibm.com/support/knowledgecenter/SSZHNR_1.0.0/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/dom/Assignment.html) (Expressionを継承)を使う. 

```xml
Expression AssignmentOperator Expression
```

| メソッド                                              | 戻り値                | 機能                                                         |
| ----------------------------------------------------- | :-------------------- | :----------------------------------------------------------- |
| `getLeftHandSide()`                                   | `Expression`          | Returns the left hand side of this assignment expression.    |
| `getOperator()`                                       | `Assignment.Operator` | Returns the operator of this assignment expression.          |
| `getRightHandSide()`                                  | `Expression`          | Returns the right hand side of this assignment expression.   |
| `propertyDescriptors(int apiLevel)`                   | `static List`         | Returns a list of structural property descriptors for this node type. |
| `setLeftHandSide(Expression expression)`              | `void`                | Sets the left hand side of this assignment expression.       |
| `setOperator(Assignment.Operator assignmentOperator)` | `void`                | Sets the operator of this assignment expression.             |
| `setRightHandSide(Expression expression)`             | `void`                | Sets the right hand side of this assignment expression.      |

### SimpleName

false, true, null以外のJavaソースコード内に存在する変数などの名前をノードとしたもの. 詳しくは[こちら](https://www.ibm.com/support/knowledgecenter/cs/SS5JSH_9.5.0/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/dom/SimpleName.html)を参照. 

| メソッド                            | 戻り値        | 機能                                                         |
| ----------------------------------- | :------------ | :----------------------------------------------------------- |
| `getIdentifier()`                   | `String`      | Returns this node's identifier.                              |
| `isDeclaration()`                   | `boolean`     | Returns whether this simple name represents a name that is being defined, as opposed to one being referenced. |
| `propertyDescriptors(int apiLevel)` | `static List` | Returns a list of structural property descriptors for this node type. |
| `setIdentifier(String identifier)`  | `void`        | Sets the identifier of this node to the given value.         |

