## What is a Relational Database?
  In simple terms, a relational database holds data. Lots of data. But why do we use a relational database if it simply holds data? Don't spreadsheets do the same thing? Well, relational databases give us some great benefits. We can imagine a relational database as multiple spreadsheets that can be linked in a special way. This linkage is important for storing and accessing data efficiently. The below example will demonstrate the importance of using a relational database to prevent wasting hard drive space.

## Example - Dealing with Data Duplication
  You're working at a brand new startup straight out of UBC's Master of Data Science program. You have a dataset that you want to store in order to do some analysis about where your customers live. Being so new, your team has decided that storing all of your data as .csv files and accessing them using a spreadsheets application is a good idea.

  SPOILER ALERT: This is not a good idea.

  The dataset below is named customers and holds data such as the name, phone number and address relating to each customer.

  Customers (name, phone_number, address)

  | id | name   | phone_number | address              |
  |----|--------|--------------|----------------------|
  | 1  | Rayce  | "1234567890" | "12345 Vancouver St" |
  | 2  | Olivia | "0987654321" | "54321 Montreal St"  |
  | 3  | Kipper | "5432167890" | "12345 Vancouver St" |

  Do you notice anything interesting about the above dataset?

  Did you notice that two of our customers have the same address? (id: 1 and id: 3)

  Data overlap is when a dataset holds the exact same data multiple times. In a larger dataset we could have significant amounts of data overlap. Even with recent advances in data storage, we're a new startup and we can barely afford coffee for the development staff, let alone the [AWS](https://aws.amazon.com "AWS") fees for storing data unncessarily!

  How do you think we could solve that problem?

  Relational databases solve this problem in a special way. Relational databases allow you to create multiple tables or *relations*, and to create a linkage between them, called a *relationship*.

  Let's go through the procedure for creating a *relationship* step by step.

## Creating a Relationship
  When creating a *relationship* we first have to identify which data is going to be duplicated. In our case, addresses are duplicated in our dataset. In order to prevent this costly data duplication, we will first separate our data into multiple datasets.

### Separating the Data
  Firstly, we'll separate our Customers dataset into a Customers and Addresses datasets.

  Customers (id, name, phone_number)

  | id | name   | phone_number |
  |----|--------|--------------|
  | 1  | Rayce  | "1234567890" |
  | 2  | Olivia | "0987654321" |
  | 3  | Kipper | "5432167890" |

  Addresses (id, address)

  | id | address              |
  |----|----------------------|
  | 1  | "12345 Vancouver St" |
  | 2  | "54321 Montreal St"  |

  By removing the address entries from the dataset and placing them into their own dataset we've removed a data duplication. We now only store one reference to "12345 Vancouver St", whereas before we had to store two.

  Now that we've removed the data duplication, how do we know which address is related with which customer?

### Defining a Relationship
  Relationships depend on *keys* to decide which *relation* relies on which other *relation(s)*. A relational database has two different types of *keys*, *primary keys* and *foreign keys*.

#### Primary keys
  Imagine a spreadsheets file, on the left hand side you have a list of numbers that grows with each row. A *primary key* is the unique identifier of a single *row* of data. Every *row* in the *relation* will have a *primary key* associated with it. Typically, the *primary key* starts at 1 and grows with the size of the *relation*. There is only one *primary key* per *row*.

  Customers (id, name, phone_number)

  | id | name   | phone_number |
  |----|--------|--------------|
  | 3  | Kipper | "5432167890" |

  In this example, "id: 3" is the primary key.

To define a relationship we use a *foreign key*. A *foreign key* is the *primary key* of another *relation*.

#### Foreign keys
  A foreign key is when you use the *primary key* of a *relation* to refer to a *row* in another *relation*. There can be multiple *foreign keys* per *row*.

  Customers (id, name, phone_number, address)

  | id | name   | phone_number | address |
  |----|--------|--------------|---------|
  | 3  | Kipper | "5432167890" | 1       |

  In this example, "address: 1" is a foreign key. This *foreign key* corresponds to the *primary key* in the Addresses *relation*.

  Addresses (id, address)

  | id | address              |
  |----|----------------------|
  | 1  | "12345 Vancouver St" |


## Finishing our Example
  Now that we know how to define a *relationship*, we can complete our *relations* and begin our analysis knowing that our data is stored without any duplications.

  Customers (id, name, phone_number, address)

  | id | name   | phone_number | address |
  |----|--------|--------------|---------|
  | 1  | Rayce  | "1234567890" | 1       |
  | 2  | Olivia | "0987654321" | 2       |
  | 3  | Kipper | "5432167890" | 1       |

  Addresses (id, address)

  | id | address              |
  |----|----------------------|
  | 1  | "12345 Vancouver St" |
  | 2  | "54321 Montreal St"  |

## Conlusion
  We've just illustrated how relational databases solve the issue of data duplication and the importance of storing data properly.

  Storing our data in a relational database not only saves us in storage fees, it also gives us access to the [*Standard Query Language* (SQL)](https://en.wikipedia.org/wiki/SQL "SQL"), a powerful language for accessing and managing data programmatically.

  Relational database's also support security levels so different database users can only access data relevant to themselves. E.g. Customer Rayce shouldn't be able to access data for Customer Olivia, and vice versa.

  Now take this knowledge into the work force and get the development team the coffee machine they deserve.
