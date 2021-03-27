---
id: 4
title: "왜 String은 대문자로 시작하고 int는 소문자로 시작할까?"
subtitle: "Primitive type vs. Reference type"
date: "2021.03.27"
tags: "java, data structure"
---

[Why is Java “String” type written in capital letter while “int” is not?](https://stackoverflow.com/questions/4006302/why-is-java-string-type-written-in-capital-letter-while-int-is-not)에 대한 stackoverflow의 답변입니다.

I am curious. Why do I have to type String myStr with a capital letter whereas I type int aNumba with a lower-case letter?

Because int is a primitive type, not a class, thus it is not directly comparable to String. The corresponding class type is Integer, spelled according to the class naming conventions.

Similar pairs of primitive and class types are

byte vs Byte
short vs Short
long vs Long
float vs Float
double vs Double
boolean vs Boolean
char vs Character


String itself is a class derived from Object, while int is a primitive.

Your confusion probably comes from the fact that String behaves in many ways like a primitive, in such that it has basic operations that can be applied to it, like the (+) concatenation, and that it does not need to be imported.

The concatenation is because it is fundamental enough to have this added operation applied, even though it is an object type.

The reason it does not need to be imported, is by default the java.lang package is imported, of which String is member.
