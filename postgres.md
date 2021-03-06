# PostgreSQL

## psql 

* list databases
* list schemas ``` \d ```
* list tables/views
* ```\x```

insert the data more handily

* \copy employee FROM stdin DELIMITER '|'
* \copy employee TO 'C:/tmp/a'

interacting with shell

* ``` \! ```
* ``` \cd ```

##  Building semi-structured database backed application

For e.g. If you are building an order management system for *all* domains then  dfining schema  for ``` orders ``` is difficult beyond basic attributes such as id, name, quantity  etc. Everything else will go into an extension column.

```
CREATE TABLE quantity_units (
  id SERIAL PRIMARY KEY,
  label text,
  display_seq int,
  is_active boolean  
);

CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  customer_id INT,
  quantity NUMBER,
  quantity_unit_id int REFERENCES quantity_units (id),
  extension xml
);

CREATE INDEX customer_id ON orders (customer_id);

```