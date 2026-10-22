# Programming for Data Science Lab (MACSE502) – Scala Programs

Lab record programs for **Programming for Data Science Lab (MACSE502)**, Fall Semester 2026,
School of Computer Science and Engineering.

This repository contains the **Scala** exercise programs (Sl. No. 18 – 25). They cover core
Scala collections, functional combinators, case classes, and data analysis with Scala libraries
(Saddle, Breeze, Spire, Vegas and Plotly-Scala).

> **Author:** `Chilla Kalyan Sai Kumar Reddy` · **Reg. No:** `26MML0052`

---

## 📋 Program Index

| Sl. No. | Week | Type | Topic | File |
|:---:|:---:|:---:|---|---|
| 18 | 9  | EP | Arrays in Scala | [`Program18_ArraysInScala.scala`](Program18_ArraysInScala.scala) |
| 19 | 10 | EP | Lists, Sets and Tuples in Scala | [`Program19_ListsSetsTuples.scala`](Program19_ListsSetsTuples.scala) |
| 20 | 11 | EP | Handling collisions and resolving conflicts in HashMaps | [`Program20_HashMapCollisions.scala`](Program20_HashMapCollisions.scala) |
| 21 | 12 | EP | Advanced functional combinators | [`Program21_FunctionalCombinators.scala`](Program21_FunctionalCombinators.scala) |
| 22 | 13 | EP | Case Classes in Scala | [`Program22_CaseClasses.scala`](Program22_CaseClasses.scala) |
| 23 | 13 | EP | Data manipulation with Saddle & visualization with Vegas | [`Program23_SaddleVegas.scala`](Program23_SaddleVegas.scala) |
| 24 | 14 | EP | Revenue analysis with Breeze & Plotly-Scala | [`Program24_BreezePlotly.scala`](Program24_BreezePlotly.scala) |
| 25 | 14 | EP | Price statistics with Spire, Saddle & Vegas | [`Program25_SpireSaddleVegas.scala`](Program25_SpireSaddleVegas.scala) |

*EP: Exercise Program*

---

## 📝 Program Details

### Program 18 – Arrays in Scala
**Problem:** Create an integer array `2, 5, 9, 14, 20` and write a function returning the sum of
its elements. Create an array of five fruit names and write a function that concatenates them
separated by commas. Finally, iterate over the integer array and print each element.

**Concepts:** `Array`, `for` loops, `mkString`, `indices`
**Key result:** Sum of elements = `50`

---

### Program 19 – Lists, Sets and Tuples
**Problem:** Create a list of the first five primes and return a new list with each element
squared. Build a set of unique characters from `"hello world"` and write a function that returns
the intersection of two sets. Create a tuple of an `Int`, a `String` and a `Boolean` and print
each element.

**Concepts:** `List.map`, `Set`, `intersect`, tuples (`_1`, `_2`, `_3`)
**Key results:**
- Squared list → `List(4, 9, 25, 49, 121)`
- Unique chars of "hello world" → `{d, e, h, l, o, r, w}` (7)
- Intersection with "scala world" → `{d, l, o, r, w}`

---

### Program 20 – HashMap Collisions and Conflict Resolution
**Problem:** Create a HashMap of student names → grades, insert a duplicate key with a different
grade, merge two HashMaps keeping the higher grade on conflicts, and handle collisions by
chaining (lists storing multiple values per bucket).

**Concepts:** `mutable.HashMap`, `Option` pattern matching, custom hash table with separate
chaining (bucket index = `name.length % 4`)
**Key results:**
- Duplicate insert `Anil -> 88` overwrites the old value (size stays 4)
- Merged map → `Anil 88, Kiran 74, Naveen 91, Pavan 92, Ravi 70`
- Chained table keeps both grades for Anil → `List(78, 88)`

---

### Program 21 – Advanced Functional Combinators
**Problem:** Create a list of integers 1 to 10. Use `filter` to keep even numbers, `map` to
multiply each element by 3, `flatMap` to pair each integer with its square, and `foldLeft` to
compute the product of all elements.

**Concepts:** `filter`, `map`, `flatMap`, `foldLeft`, combinator chaining
**Key results:**
- Evens → `List(2, 4, 6, 8, 10)`
- Product (`foldLeft`) → `3628800`
- Chained `filter → map → foldLeft` (sum of tripled evens) → `90`

---

### Program 22 – Case Classes
**Problem:** Define a case class `Person(name, age, city)` and create a list of five people.
Write functions to filter people older than 30, group people by city, transform each person into
a descriptive string, and sort people by age in ascending order.

**Concepts:** `case class`, `filter`, `groupBy`, `map` with string interpolation, `sortBy`

---

### Program 23 – Saddle + Vegas
**Problem:** Load the fruit prices dataset into a Saddle `Frame`, filter the rows for **Apple**,
calculate the average apple price, and visualize the apple price trend over time with Vegas.

**Concepts:** Saddle `Frame` / `Series`, `filter`, `reindex`, Vega-Lite line chart
**Key result:** Average apple price = `Rs. 128.38`
**Output:** `apple_price_trend.html` (interactive line chart)

---

### Program 24 – Breeze + Plotly-Scala
**Problem:** Store price and quantity as Breeze `DenseVector`s, compute the revenue of every record
(element-wise multiplication), compute the total revenue per fruit, and display it as an
interactive bar chart with Plotly-Scala.

**Concepts:** `DenseVector`, element-wise product `*:*`, dot product with a 0/1 mask, Plotly `Bar`
**Output:** `fruit_revenue.html` (interactive bar chart)

---

### Program 25 – Spire + Saddle + Vegas
**Problem:** Load the dataset with Saddle, group prices by fruit, compute the **exact** mean and
variance of prices using Spire `Rational` numbers (no floating-point rounding), and visualize the
price trend of every fruit over time with Vegas.

**Concepts:** Spire `Rational`, exact arithmetic, Saddle filtering, multi-series Vegas line chart
**Output:** `fruit_price_trends.html` (interactive multi-line chart)

---

## 📊 Dataset – `fruit_prices.csv`

Used by Programs 23, 24 and 25. Monthly prices (Jan – Jun 2026) for four fruits.

| Column | Type | Description |
|---|---|---|
| `Date` | Date (`yyyy-MM-dd`) | Month of the record |
| `Fruit` | String | Apple, Banana, Mango, Orange |
| `Price` | Double | Price per kg (Rs.) |
| `Quantity` | Int | Quantity sold |

24 rows × 4 columns. Keep this file in the project root (the working directory when you run).

---

## ⚙️ Requirements

- **JDK 8** (recommended for Scala 2.11)
- **Scala 2.11.12**
- **sbt** 1.x

Programs 18–22 use only the Scala standard library.
Programs 23–25 need the libraries below — add them to `build.sbt`:

```scala
name := "pds-lab-scala"
version := "1.0"
scalaVersion := "2.11.12"

libraryDependencies ++= Seq(
  "org.scala-saddle" %% "saddle-core"   % "1.3.4",   // data frames
  "org.vegas-viz"    %% "vegas"         % "0.3.11",  // Vega-Lite charts
  "org.scalanlp"     %% "breeze"        % "0.13.2",  // linear algebra
  "org.plotly-scala" %% "plotly-render" % "0.5.4",   // Plotly charts
  "org.typelevel"    %% "spire"         % "0.13.0"   // exact numeric types
)
```

---

## ▶️ How to Run

Clone the repository:

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

**Programs 18 – 22** (standard library only) – run directly with the Scala runner:

```bash
scala Program18_ArraysInScala.scala
```

**Any program with sbt** (required for 23 – 25):

```bash
sbt "runMain Program23_SaddleVegas"
sbt "runMain Program24_BreezePlotly"
sbt "runMain Program25_SpireSaddleVegas"
```

> If you use sbt, place the `.scala` files in `src/main/scala/` (or keep them in the root — sbt
> also compiles sources in the base directory).

Programs 23 – 25 write their charts as HTML files in the project root. Open them in any browser
to interact with the charts.

---

## 📁 Repository Structure

```
.
├── Program18_ArraysInScala.scala
├── Program19_ListsSetsTuples.scala
├── Program20_HashMapCollisions.scala
├── Program21_FunctionalCombinators.scala
├── Program22_CaseClasses.scala
├── Program23_SaddleVegas.scala
├── Program24_BreezePlotly.scala
├── Program25_SpireSaddleVegas.scala
├── fruit_prices.csv
├── build.sbt
└── README.md
```

Generated after running:

```
apple_price_trend.html      ← Program 23
fruit_revenue.html          ← Program 24
fruit_price_trends.html     ← Program 25
```

---

## 🧰 Libraries Used

| Library | Purpose | Used in |
|---|---|---|
| [Saddle](https://github.com/saddle/saddle) | Data frames and series (like pandas) | 23, 25 |
| [Vegas](https://github.com/vegas-viz/Vegas) | Declarative Vega-Lite visualizations | 23, 25 |
| [Breeze](https://github.com/scalanlp/breeze) | Numerical computing and linear algebra | 24 |
| [Plotly-Scala](https://github.com/alexarchambault/plotly-scala) | Interactive Plotly charts | 24 |
| [Spire](https://github.com/typelevel/spire) | Exact numeric types (`Rational`) | 25 |

---

## 📄 License

This repository is shared for academic purposes as part of the MACSE502 lab record.
