---
layout: single
title: StringBuffer
categories: READING
tag: 
---

public final class StringBuffer
extends Object
implements Serializable, CharSequence
A thread-safe, mutable sequence of characters. A string buffer is like a String, but can be modified. __At any point in time__ it contains some particular sequence of characters, but the length and content of the sequence can be changed through certain method calls.
String buffers are safe for use by multiple threads. __The methods are synchronized where necessary so that all the operations on any particular instance behave as if they occur in some serial order that is consistent with the order of the method calls made by each of the individual threads involved.__

The principal operations on a StringBuffer are the append and insert methods, which are overloaded so as to accept data of any type. Each effectively converts a given datum to a string and then appends or inserts the characters of that string to the string buffer. The append method always adds these characters at the end of the buffer; the insert method adds the characters at a specified point.

__For example, if z refers to a string buffer object whose current contents are "start", then the method call z.append("le") would cause the string buffer to contain "startle", whereas z.insert(4, "le") would alter the string buffer to contain "starlet".__

In general, if sb refers to an instance of a StringBuffer, then sb.append(x) has the same effect as sb.insert(sb.length(), x).

Whenever an operation occurs involving a source sequence (such as appending or inserting from a source sequence), this class synchronizes only on the string buffer performing the operation, not on the source. Note that while StringBuffer is designed to be safe to use concurrently from multiple threads, if the constructor or the append or insert operation is passed a source sequence that is shared across threads, the calling code must ensure that the operation has a consistent and unchanging view of the source sequence for the duration of the operation. This could be satisfied by the caller holding a lock during the operation's call, by using an immutable source sequence, or by not sharing the source sequence across threads.

Every string buffer has a capacity. As long as the length of the character sequence contained in the string buffer does not exceed the capacity, it is not necessary to allocate a new internal buffer array. If the internal buffer overflows, it is automatically made larger.

Unless otherwise noted, passing a null argument to a constructor or method in this class will cause a NullPointerException to be thrown.

As of release JDK 5, this class has been supplemented with an equivalent class designed for use by a single thread, StringBuilder. The StringBuilder class should generally be used in preference to this one, as it supports all of the same operations but it is faster, as it performs no synchronization.   

*At any point in time : 어느 시점에서도    

*The methods are synchronized where necessary so that all the operations on any particular instance behave as if they occur in some serial order that is consistent with the order of the method calls made by each of the individual threads involved.   
: 메소드들은 임의의 특정 인스턴스에 대한 모든 동작들이 관련된 각각의 개별 스레드들에 의해 행해지는 메소드 호출들의 순서와 일치하는 일부 직렬 순서로 발생하는 것처럼 동작하도록 필요한 경우 동기화된다.   
: (The methods are synchronized) 중심 내용 - 여기까지만 알면된다. 뒤에는 전부 메소드가 동기화 되는 것에 대한 상황 설명이고 또 이 설명의 상황 설명.   
/ where necessary(where은 관계 부사절로 앞에 The ~ syncronized 란 절을 꾸며준다 where it is necessary의 줄임) 필요한 경우 / so that ~하기 위해 / all the operations on any particular instance behave 모든 동작들이 (~에 대한 특정 인스턴스에) 행해지기 위해서 / as if 마치 ~ 인 것 처럼 / they occur in some serial order 그것들(메소드들)이 직렬 순서로 발생하는.
/ that (앞에 직렬 순서에 대한 설명) is consistent with the order of the method calls (앞의 직렬 순서는) 일치한다 메소드 호출의 순서와   
/ (메소드 호출 순서에 대한 설명) made by each of the individual thtreads involved. (앞의 호출 순서는) 관련있는 각각의 개별 쓰레드들에 의해 만들어진

*For example, if z refers to a string buffer object whose current contents are "start", then the method call z.append("le") would cause the string buffer to contain "startle", whereas z.insert(4, "le") would alter the string buffer to contain "starlet".
: 
