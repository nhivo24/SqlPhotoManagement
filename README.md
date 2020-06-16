# CREATE TABLE

```
create database photomanagement;

use photomanagement;

create table users (
	id bigint primary key auto_increment,
    email varchar(50),
    password varchar(255),
	role varchar(50),
    created_at datetime,
    updated_at datetime                  
);

create table categories (
	id bigint primary key auto_increment,
    name varchar(50),
    created_at datetime,
    updated_at datetime
);

     
create table photos (
	id bigint primary key auto_increment,
    title varchar(100),
    category_id bigint,
    image varchar(100),
    created_at datetime,
    updated_at datetime,
    foreign key (category_id) references categories(id)
);

     
create table tags (
	id bigint primary key auto_increment,
    name varchar(50),
    created_at datetime,
    updated_at datetime
);

create table taggable(
	tag_id bigint,
    photo_id bigint,
    created_at datetime,
    updated_at datetime,
    primary key (tag_id, photo_id),
    foreign key (tag_id) references tags(id),
    foreign key (photo_id) references photos(id)
);


create table photo_descriptions (
	photo_id bigint,
    content varchar(100),
    created_at datetime,
    updated_at datetime,
    foreign key (photo_id) references photos(id)
);

```
# INSERT DATA
```

insert into users(email,password,role) 
value('vothinhi2410@gmail.com','nhi','admin'),
	 ('vonhi2410@gmail.com','vonhi','user');
     
insert into categories(name) 
value('Banh kem'),
	 ('banh mi');
     
insert into photos(title, category_id,image) 
value('Nice',1,'nhi.jpg'),
	 ('alone',2,'dung.png');
     
insert into tags(name) 
value('lovely'),
	 ('lonely'),
	 ('broken'),
	 ('Miss');
     
insert into taggable(tag_id,photo_id) 
value (1,1),
	  (2,1),
	  (2,2),
	  (3,2),
	  (3,1);
      
insert into photo_descriptions(content) 
value('Have a nice day!');
	select * from photos,categories;
    ```
# QUERY

```

select p.title, c.name ,(select content from photo_descriptions  where photo_id = p.id) as descriptions
,(select group_concat(t.name) from tags as t, taggable as tg where tg.tag_id = t.id and tg.photo_id = p.id  ) as  tags
from photos as p , categories as c where p.category_id = c.id ;

```
