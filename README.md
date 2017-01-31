# mongodb-query


## 1. Membuat database academic

input:

```
use academic
```

output:

```
switched to db academic
```

## 2. menampilkan semua collections dan data dalam database

input:

```
show dbs
```

output:

```
admin  0.000GB
local  0.000GB
```

input:

```
show collections
```

output:

```

```

## 3. Membuat atau mengaktifkan database

input:

```
use academic
```

output:

```
switched to db academic

```

## 4. Membuat collection departments

input:

```
db.createCollection(departments)
```

output:

```
{ "ok" : 1 }
```

## 5. Membuat collection students

input:

```
db.createCollection(students)
```

output:

```
{ "ok" : 1 }
```

## 6. melihat struktur collection students

input:

```
db.students.find()
```

output:

```

```

## 7. Menginputkan 5 data ke dalam collection departments

Input:

```
db.departments.insert([
  {code: 1, name: 'Psychology' , major: ['Klinis Dewasa', 'Klinis Anak', 'Sosial', 'Pendidikan'] },
  {code: 2, name: 'Sastra', major: ['Arab', 'Jerman', 'Belanda', 'Jawa']},
  {code: 3, name: 'FISIP', major: ['HI', 'Kriminologi', 'Sosiologi', 'Komunikasi']},
  {code: 4, name: 'Hukum', major: ['Hukum perdata', 'Hukum Syariah']},
  {code: 5, name: 'Ekonomi', major: ['Ilmu Ekonomi', 'Bisnis', 'Akuntasi']}
  ])
```

Output:

```
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 5,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})
```

## 8. Menginputkan 3 data ke dalam collection students beserta reference ke departments

Input:

```
db.students.insert([
  {studentId: '2109394329', name: 'Andi Santosa', address: 'Jakarta', departments: {
    $ref: 'departments',
    $id: ObjectId("589015065f3ac21a0f329307"),
    $db: 'academic'
    }},
  {studentId: '43454399985', name: 'Budi Salosa', address: 'Depok', departments: {
    $ref: 'departments',
    $id: ObjectId("589015065f3ac21a0f329309"),
    $db: 'academic'
    }},
  {studentId: '8973494329', name: 'Gaga Dogosa', address: 'Tangerang', departments: {
    $ref: 'departments',
    $id: ObjectId("589015065f3ac21a0f32930b"),
    $db: 'academic'
    }}  
  ])
```

Output:

```
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 3,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})
```

## 9. Melihat isi collection students

Input:

```
db.students.find()
```

Output:

```
{ "_id" : ObjectId("589018ad5f3ac21a0f32930c"), "studentId" : "2109394329", "name" : "Andi Santosa", "address" : "Jakarta", "departments" : DBRef("departments", ObjectId("589015065f3ac21a0f329307"), "academic") }
{ "_id" : ObjectId("589018ad5f3ac21a0f32930d"), "studentId" : "43454399985", "name" : "Budi Salosa", "address" : "Depok", "departments" : DBRef("departments", ObjectId("589015065f3ac21a0f329309"), "academic") }
{ "_id" : ObjectId("589018ad5f3ac21a0f32930e"), "studentId" : "8973494329", "name" : "Gaga Dogosa", "address" : "Tangerang", "departments" : DBRef("departments", ObjectId("589015065f3ac21a0f32930b"), "academic") }
```

## 10. menampilkan key name dan address dalam collection students

Input:

```
db.students.find({},{name: true, address: true})
```

Output:

```
{ "_id" : ObjectId("589018ad5f3ac21a0f32930c"), "name" : "Andi Santosa", "address" : "Jakarta" }
{ "_id" : ObjectId("589018ad5f3ac21a0f32930d"), "name" : "Budi Salosa", "address" : "Depok" }
{ "_id" : ObjectId("589018ad5f3ac21a0f32930e"), "name" : "Gaga Dogosa", "address" : "Tangerang" }
```

## 11. menampilkan key studentId, name, dan  address dari data students

Input:

```
db.students.findOne({},{name: true, address: true, studentId: '43454399985'})
```

Output:

```
{
	"_id" : ObjectId("589018ad5f3ac21a0f32930c"),
	"studentId" : "2109394329",
	"name" : "Andi Santosa",
	"address" : "Jakarta"
}
```

## 12. menampilkan semua data student secara urut berdasarkan name dengan sort() secara ascending maupun ascending maupun descending

Input: (DSC)

```
db.students.find().sort({name:1})
```

Output:

```
{ "_id" : ObjectId("589018ad5f3ac21a0f32930c"), "studentId" : "2109394329", "name" : "Andi Santosa", "address" : "Jakarta", "departments" : DBRef("departments", ObjectId("589015065f3ac21a0f329307"), "academic") }
{ "_id" : ObjectId("589018ad5f3ac21a0f32930d"), "studentId" : "43454399985", "name" : "Budi Salosa", "address" : "Depok", "departments" : DBRef("departments", ObjectId("589015065f3ac21a0f329309"), "academic") }
{ "_id" : ObjectId("589018ad5f3ac21a0f32930e"), "studentId" : "8973494329", "name" : "Gaga Dogosa", "address" : "Tangerang", "departments" : DBRef("departments", ObjectId("589015065f3ac21a0f32930b"), "academic") }
```

Input: (ASC)

```
db.students.find().sort({name:-1})

```

Output:

```
{ "_id" : ObjectId("589018ad5f3ac21a0f32930e"), "studentId" : "8973494329", "name" : "Gaga Dogosa", "address" : "Tangerang", "departments" : DBRef("departments", ObjectId("589015065f3ac21a0f32930b"), "academic") }
{ "_id" : ObjectId("589018ad5f3ac21a0f32930d"), "studentId" : "43454399985", "name" : "Budi Salosa", "address" : "Depok", "departments" : DBRef("departments", ObjectId("589015065f3ac21a0f329309"), "academic") }
{ "_id" : ObjectId("589018ad5f3ac21a0f32930c"), "studentId" : "2109394329", "name" : "Andi Santosa", "address" : "Jakarta", "departments" : DBRef("departments", ObjectId("589015065f3ac21a0f329307"), "academic") }
```

## 13. Menampilkan semua data departements secara urut berdasarkan name secara ascending maupun descending

Input: (ASC)

```
db.departments.find().sort({name:1})

```

Output:

```
{ "_id" : ObjectId("589015065f3ac21a0f32930b"), "code" : 5, "name" : "Ekonomi", "major" : [ "Ilmu Ekonomi", "Bisnis", "Akuntasi" ] }
{ "_id" : ObjectId("589015065f3ac21a0f329309"), "code" : 3, "name" : "FISIP", "major" : [ "HI", "Kriminologi", "Sosiologi", "Komunikasi" ] }
{ "_id" : ObjectId("589015065f3ac21a0f32930a"), "code" : 4, "name" : "Hukum", "major" : [ "Hukum perdata", "Hukum Syariah" ] }
{ "_id" : ObjectId("589015065f3ac21a0f329307"), "code" : 1, "name" : "Psychology", "major" : [ "Klinis Dewasa", "Klinis Anak", "Sosial", "Pendidikan" ] }
{ "_id" : ObjectId("589015065f3ac21a0f329308"), "code" : 2, "name" : "Sastra", "major" : [ "Arab", "Jerman", "Belanda", "Jawa" ] }
```

Input: DSC

```
db.departments.find().sort({name:-1})

```

Output:

```
{ "_id" : ObjectId("589015065f3ac21a0f329308"), "code" : 2, "name" : "Sastra", "major" : [ "Arab", "Jerman", "Belanda", "Jawa" ] }
{ "_id" : ObjectId("589015065f3ac21a0f329307"), "code" : 1, "name" : "Psychology", "major" : [ "Klinis Dewasa", "Klinis Anak", "Sosial", "Pendidikan" ] }
{ "_id" : ObjectId("589015065f3ac21a0f32930a"), "code" : 4, "name" : "Hukum", "major" : [ "Hukum perdata", "Hukum Syariah" ] }
{ "_id" : ObjectId("589015065f3ac21a0f329309"), "code" : 3, "name" : "FISIP", "major" : [ "HI", "Kriminologi", "Sosiologi", "Komunikasi" ] }
{ "_id" : ObjectId("589015065f3ac21a0f32930b"), "code" : 5, "name" : "Ekonomi", "major" : [ "Ilmu Ekonomi", "Bisnis", "Akuntasi" ] }

```

## 14. Mencari data student dengan name

Input:

```
db.students.findOne({name: 'Andi Santosa'})

```

Output:

```
{
	"_id" : ObjectId("589018ad5f3ac21a0f32930c"),
	"studentId" : "2109394329",
	"name" : "Andi Santosa",
	"address" : "Jakarta",
	"departments" : DBRef("departments", ObjectId("589015065f3ac21a0f329307"), "academic")
}
```
