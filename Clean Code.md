**Author name: Robert C Martin**

**The Only Valid Measurement of Code Quality : WTFs/minute**

**Why Reading this book : we want to be a better programmer.**

**There will always be Code**
No matter, how much level of abstraction of our languages increases , there will always be code. we ultimately have to express our requirements to machines.

**Bad code let a company down**

There was a killer app in 1980's, which was highly popular. but as the company adding more features to it, code messed up and become worse than before. As obvious everyone shut down the product in frustration. The company went out of business a short time after that.

**LeBlanc’s law: Later equals never.**

**The Total Cost of Owning a Mess**

![[/images/productivity_vs_time.png]]

Messy code slows down software development over time. At first, things move fast, but as the mess grows, even small changes break other parts of the code. This makes progress very slow (Tends to zero). To fix it, managers often hire more people, but new team members don’t understand the system well and accidentally make things worse. As a result, the mess keeps growing, and the team gets less and less done.

**spending time keeping your code clean is not just cost effective; it’s a matter of professional survival.**

**Most managers want good code, even when they are obsessing about the schedule.**
They may defend the schedule and requirements with passion; but that’s their job. It’s your job to defend the code with equal passion.

**You will not make the deadline by making the mess.**
Indeed, the mess will slow you down instantly, and will force you to miss the deadline. The only way to make the deadline—the only way to go fast—is to keep the code as clean as possible at all times.

**Clean code comes from a practiced "code-sense" that guides programmers in turning messy code into elegant solutions.**

**beautiful code makes the language look like it was made for the problem! - Ward Cunningham, inventor of Wiki**

**The next time you write a line of code, remember you are an author, writing for readers who will judge your effort.**

**The Boy Scout Rule** 
Code should stay clean over time, not just when it's first written. Like the Boy Scouts say:  
**“Leave the campground cleaner than you found it.”**

That means, every time you work on code, improve it just a little — maybe rename a variable, break a big function into smaller ones, or remove a bit of duplication.

If everyone does this, the codebase will keep getting better instead of worse. That’s what being a professional is all about: **continuous improvement.**

**Naming Suggestions:**
1. **Use Intention-Revealing Names.**
	Good names in code should clearly show **what** something is, **why** it exists, and **how** it’s used — without needing comments.

	For example:  
	`int d; // elapsed time in days`  
	This is unclear. A better name:  
	`int elapsedTimeInDays;`

	Descriptive names make code easier to read and change.

	Example of unclear code:

	``` java
	public List<int[]> getThem() {     
		List<int[]> list1 = new ArrayList<>();     
		for (int[] x : theList)         
			if (x[0] == 4)             
				list1.add(x);     
		return list1; 
	}
	```

	It’s hard to understand because the names don’t explain:

	- What is in `theList`?
    
	- What does `x[0] == 4` mean?
    
	- What is `list1`?
    
	Better names would answer these questions directly, making the code obvious and easier to maintain.

	Improved with clear names (like in a minesweeper game):

``` java
	public List<int[]> getFlaggedCells() {     
		List<int[]> flaggedCells = new ArrayList<>();     
		for (int[] cell : gameBoard)         
			if (cell[STATUS_VALUE] == FLAGGED)             
				flaggedCells.add(cell);     
		return flaggedCells; 
	}
```

	Even better with a Cell class:

``` java
	public List<Cell> getFlaggedCells() {     
		List<Cell> flaggedCells = new ArrayList<>();     
		for (Cell cell : gameBoard)         
			if (cell.isFlagged())             
				flaggedCells.add(cell);     
		return flaggedCells; 
	}	
```

2.  **Avoid Disinformation**

	Programmers should avoid names that mislead or confuse. For example:
	
	- Don’t use `hp` for hypotenuse — it may confuse readers familiar with Unix terms like HP-UX.
    
	- Don’t name a group of accounts `accountList` if it’s not a List. Better names: `accountGroup` or just `accounts`.
    

	Names that look similar but mean different things can confuse:

	- `XYZControllerForEfficientHandlingOfStrings` vs `XYZControllerForEfficientStorageOfStrings` — too similar to quickly tell apart.
    

	Also, avoid tricky names like lowercase `l` or uppercase `O` since they look like `1` and `0`:

```java
	int a = l;
	if (O == l)
	    a = O1;
	else
	    l = 01;
```
``
	This is confusing. Instead, use clear, distinct names to prevent mistakes no special fonts or comments needed.

3. **Make Meaningful Distinctions**

	Don’t create different names just to please the compiler. **Every name should have a distinct and meaningful purpose.**

	 Bad Practices:
	- **Misspellings:** Using `klass` instead of `class` just to avoid conflicts is bad practice.
	- **Numbered names:** Names like `a1`, `a2` don’t explain anything:
    

```java
	public static void copyChars(char a1[], char a2[]) {
	    for (int i = 0; i < a1.length; i++) {
	        a2[i] = a1[i];
	    }
	}
```
``
	Better:
``
```java
	public static void copyChars(char[] source, char[] destination) { ... }
```
``
	 **Avoid Noise Words**
``
	Words like `Info`, `Data`, `Object` add no real meaning:``
	- `Product`, `ProductInfo`, `ProductData` — all sound the same.``
	- `Customer` vs `CustomerObject` — what’s the difference?
``
	Similarly, words like `variable` or `table` are unnecessary:
	- `NameString` vs `Name` — the extra word "String" doesn’t help.
	- `moneyAmount` vs `money` — redundant.
``
	 **Real Example of Confusion:**

```java
	getActiveAccount()
	getActiveAccounts()
	getActiveAccountInfo()
```
``
	These look different but don’t clarify what each does.
``
	Make names that **clearly show differences**. If you have to choose between similar words, ensure each one describes a unique purpose or behavior.

4. **Use Pronounceable Names**

	Use names that are easy to pronounce. If you can’t say a name easily, it’s hard to discuss it with others — and coding is a team effort.

	For example, a company used this:

```java
	private Date genymdhms;  // generation year, month, day, hour, minute, second
	private Date modymdhms;
	private final String pszqint = "102";
```
``
	These are hard to say or understand.
``
	Better:

```java
	private Date generationTimestamp;
	private Date modificationTimestamp;
	private final String recordId = "102";
```
``
	Now you can discuss the code clearly, e.g.,  
	**“The generation timestamp is set to tomorrow — is that right?”**
``
	Choose names that are easy to read, say, and understand. It makes collaboration much smoother.

5. **Use Searchable Names**

	Avoid single-letter names and raw numbers in code because they are hard to search for.

	For example:
	
	``` java
	for (int j=0; j<34; j++) {   
	  s += (t[j]*4)/5; 
	}
	```

	It’s unclear and difficult to find where `4` or `5` is used.

	Better:
	
	``` java
	int realDaysPerIdealDay = 4; 
	const int WORK_DAYS_PER_WEEK = 5; 
	for (int j=0; j < NUMBER_OF_TASKS; j++) {     
		int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;     
		int realTaskWeeks = realTaskDays / WORK_DAYS_PER_WEEK;     
		sum += realTaskWeeks; 
	}
	```

	Now, `WORK_DAYS_PER_WEEK` is easy to search, unlike the number `5`.  
	Also, names like `e` or `j` are okay **only in small, short methods** — otherwise, use meaningful names.

	Use clear, descriptive names instead of numbers or short letters so your code is easier to read, understand, and search.

5. **Avoid Encodings**

	Don’t add extra symbols or prefixes to names to show type or scope — it only makes code harder to read and maintain.

	**Examples:**

	- **Hungarian Notation:** Adding types in names like `phoneString` — if the type changes, the name becomes wrong.
    
	- **Member Prefixes:** Using `m_` before member variables:
    
```java
	private String m_dsc;
```
``
	Better:

```java
	private String description;
```
``
	Modern languages like Java check types, and IDEs highlight members, so extra prefixes aren’t needed.
``
	**For Interfaces:**
``
	Instead of:``
	- `IShapeFactory` (interface)``
	- `ShapeFactory` (implementation)
``
	Better:``
	- `ShapeFactory` (interface)``
	- `ShapeFactoryImpl` (implementation)
``
	Avoid encoded names. Use **clear, simple, and meaningful names** — no prefixes, no extra codes.

6. **Avoid Mental Mapping**

	Names should be clear so readers don’t have to guess or mentally translate them.
	- **Single-letter names** like `i`, `j` are okay for small loop counters, but not elsewhere.
	- Avoid names like `c` or `r` that force readers to remember what they stand for.

	A **smart programmer** might remember these easily, but a **professional programmer** writes clear code so others don’t have to.

	**Naming Rules:**
	- **Class names:** Use nouns like `Customer`, `WikiPage`, `Account`. Avoid vague words like `Manager`, `Processor`, `Data`, `Info`.
	- **Method names:** Use verbs like `postPayment()`, `deletePage()`, `save()`.

	For getters, setters, and checks:

```java
	employee.getName();
	customer.setName("Mike");
	if (paycheck.isPosted()) { ... }
```
``
	For constructors with different arguments, use **static factory methods**:

```java
	Complex point = Complex.fromRealNumber(23.0);
```
``
	instead of:

```java
	Complex point = new Complex(23.0);
```
``
	Write code that’s easy to understand — without forcing others to mentally map names to meanings.

7. **Don't Be Cute**

	Avoid using clever or joke names in code — they can confuse others.

	For example:
	- `HolyHandGrenade()` → unclear
	- `DeleteItems()` → clear

	Don’t use slang or jokes like:
	- `whack()` instead of `kill()`
	- `eatMyShorts()` instead of `abort()`

8. **Pick One Word Per Concept**

	Use the **same word for the same concept** throughout your code to avoid confusion.

	For example, don’t mix:
	- `fetch`, `retrieve`, `get` — for similar actions across different classes.

	It forces others to remember who wrote the code to recall the correct term.

	Also, be consistent with terms like:
	- `Manager`, `Controller`, `Driver`

	For example:
	- Why have both `DeviceManager` and `ProtocolController`? Are they both managers or controllers?

	Stick to a **consistent naming pattern**. It helps others understand and use your code easily without guessing.

