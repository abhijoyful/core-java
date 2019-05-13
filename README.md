<h2>1. Introduction</h2>
In this tutorial, we will describe and demonstrate what causes <em>NumberFormatException</em> in Java. Further, we will also learn how to avoid or deal with it. <strong>Java throws <i>NumberFormatException </i>when it cannot convert a string to a number type.</strong> It is a runtime, or in other words an unchecked, exception. Hence, Java does not force us to handle or declare it. <strong><em>NumberFormatException</em> is often a result of programming ignorance, mostly predictable</strong>.
<h2>2. Causes of <em>NumberFormatException</em></h2>
There are various issues which cause <em>NumberFormatException</em>. For instance, some constructors and methods in Java throw this exception. Let's discuss most of them.
<h3><strong>2.1. Non-Numeric Data Passed to Constructor</strong></h3>
Let's look at an attempt to construct an integer or double object with non-number data. Here we are trying to create objects of number type with <em>Integer</em> and <em>Double</em> constructor.

This will throw <em>NumberFormatException</em>:
<pre class="brush: java; gutter: true">Integer aIntegerObj = new Integer("one");
Double doubleDecimalObj = new Double("two.2");</pre>
Let's see what happened when we passed invalid input "one" to <em>Integer</em> constructor in line 1. Here is the stack trace:
<pre class="brush: java; gutter: true">Exception in thread "main" java.lang.NumberFormatException: For input string: "one"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:65)
	at java.lang.Integer.parseInt(Integer.java:580)
	at java.lang.Integer.&lt;init&gt;(Integer.java:867)
	at MainClass.main(MainClass.java:11)</pre>
It threw <em>NumberFormatException</em>. The <em>Integer</em> constructor failed while trying to understand input using <em>parseInt() </em>internally.

Correct Usage:
<pre class="brush: java; gutter: true">Integer aIntegerObj = new Integer("1");
Double doubleDecimalObj = new Double("2.2");</pre>
<h3><strong>2.2. Parsing Strings Containing Non-Numeric Data</strong></h3>
In this example, we will attempt to parse a string containing non-number data. For instance, we will use parsing methods like <em>par</em><em>seInt(), parseDouble(), </em><em>valueOf()</em> and <em>decode()</em><em>.</em>

This will throw <em>NumberFormatException</em>:
<pre class="brush: java; gutter: true">int aIntPrim = Integer.parseInt("two");
double aDoublePrim = Double.parseDouble("two.two");
Integer aIntObj = Integer.valueOf("three");
Long decodeInteger = Long.decode("64403L");</pre>
Correct Usage:
<pre class="brush: java; gutter: true">int aIntPrim = Integer.parseInt("2");
double aDoublePrim = Double.parseDouble("2.2");
Integer aIntObj = Integer.valueOf("3");
Long decodeInteger = Long.decode("64403");</pre>
<h3><strong>2.3. Passing String with Extraneous Characters</strong></h3>
This one will be an attempt to initialize/parse a string with some extraneous data, like<strong> space </strong>or <strong>special characters </strong>(except minus).

This will throw <em>NumberFormatException</em>:
<pre class="brush: java; gutter: true">Short shortInt = new Short("2 ");
int bIntPrim = Integer.parseInt("6_000");</pre>
Correct Usage:
<pre class="brush: java; gutter: true">Short shortInt = new Short("2 ".trim());
int bIntPrim = Integer.parseInt("6_000".replaceAll("_", ""));
int bIntPrim = Integer.parseInt("-6000");</pre>
We can notice here in line 3 that negative numbers are allowed.
<h3><strong>2.4. Locale-Specific Number Formats</strong></h3>
Let's see a special case of locale-specific numbers. In European regions, a comma may represent a decimal. For example, "4000,1 " may represent decimal number "4000.1".

This will throw <em>NumberFormatException</em>:
<pre class="brush: java; gutter: true">double aDoublePrim = Double.parseDouble("4000,1");</pre>
But we need to allow comma and avoid exception in this case. To make it possible, Java needs to understand the comma here as a decimal.

Correct Usage:

This is how we allow comma for the European region. Let's do it for France locale, as an example:
<pre class="brush: java; gutter: true">NumberFormat numberFormat = NumberFormat.getInstance(Locale.FRANCE);
Number parsedNumber = numberFormat.parse(4000,1);
double parsedDouble = parsedNumber.doubleValue();  // returns 4000.1
int parsedInt = parsedNumber.intValue();  // returns 4000
</pre>
<h2>3. Best Practices</h2>
Let's talk about a few good practices. This will help us in dealing with <em>NumberFormatException</em>.
<ol>
 	<li><strong>We should not try to convert alphabets or special characters into numbers</strong>. Java Number API cannot do that.</li>
 	<li><strong>We may want to validate input using regular expressions. Consequently, throw the exception for the invalid characters</strong>.</li>
 	<li>We can optimize input for expected known issues. This is done with methods like <em>trim()</em>, <em>replaceAll()</em> etc. This is discussed in <em>Section 2.3</em>.</li>
 	<li>In some cases, however, special characters in input may be valid. Therefore, we do special processing for that. This is discussed in <em>Section 2.4</em>.</li>
</ol>
<h2>4. Conclusion</h2>
In this tutorial, we discussed <em>NumberFormatException</em> from many dimensions. Further, we learned that we handle this exception when we are responsible for the input. Otherwise, we report (throw) it to the caller. Or, we declare it at the least. We talked about the causes of this exception and the remedies. In conclusion, we can say that understanding this exception will help us in creating robust applications.
