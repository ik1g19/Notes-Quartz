#java 

---

```java
String str = "journaldev";
		
//string to char array
char[] chars = str.toCharArray();
```

You can then pass an array of chars to a string constructor to get a string back

```java
String str = new String(chars);
```