---
layout: post
title: "Ruby Comparison Operators"
date: 2012-11-24 07:59
comments: true
categories: [ruby, operators, triple equal, double equal]
---

There has been lots of questions on the comparison operators. So we yanked it for you..

<table class="src" border="1" cellpadding="5" cellspacing="0" width="100%">
<tbody><tr>
<th width="10%">Operator</th><th width="45%">Description</th><th>Example</th>
</tr>
<tr>
<td>==</td><td> Checks if the value of two operands are equal or not, if yes then condition becomes true.</td><td> (a == b) is not true. </td>
</tr>
<tr>
<td>!=</td><td> Checks if the value of two operands are equal or not, if values are not equal then condition becomes true.</td><td> (a != b) is true. </td>
</tr>
<tr>
<td>&gt;</td><td> Checks if the value of left  operand is greater than the value of right operand, if yes then condition becomes true.</td><td> (a &gt; b) is not true. </td>
</tr>
<tr>
<td>&lt;</td><td> Checks if the value of left  operand is less than the value of right operand, if yes then condition becomes true.</td><td> (a &lt; b) is true. </td>
</tr>
<tr>
<td>&gt;=</td><td> Checks if the value of left  operand is greater than or equal to the value of right operand, if yes then condition becomes true.</td><td> (a &gt;= b) is not true. </td>
</tr>
<tr>
<td>&lt;=</td><td> Checks if the value of left  operand is less than or equal to the value of right operand, if yes then condition becomes true.</td><td> (a &lt;= b) is true. </td>
</tr>
<tr>
<td>&lt;=&gt;</td><td> Combined comparison operator. Returns 0 if first operand equals second, 1 if first operand is greater than the second and -1 if first operand is less than the second.</td><td> (a &lt;=&gt; b)  returns -1. </td>
</tr>
<tr>
<td>===</td><td> Used to test equality within a when clause of a <i>case</i> statement.</td><td> (1...10) === 5 returns true. </td>
</tr>
<tr>
<td><b>.eql?</b></td><td>True if the receiver and argument have both the same type and equal values.</td><td> 1
== 1.0 returns true, but 1<b>.eql?</b>(1.0) is false.</td>
</tr>
<tr>
<td><b>equal?</b></td><td>True if the receiver and argument have the same object id.</td><td> 1
== 1.0 returns true, but 1<b>.eql?</b>(1.0) is false.</td>
</tr>
</tbody></table>


There's more here at the [Source Link](http://www.tutorialspoint.com/ruby/ruby_operators.htm)

Any questions on this, please feel free to ask. We're here to help...
