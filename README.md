# MongoDB_Task-1

In this Document using mongodb compass applicatiob I have given the Queries that I used to get data,

Here the commands i executed for each Questions separately:

Find all the information about each products
db.getCollection('Product_Data').find({});

Find the product price which are between 400 to 800
db.getCollection('Product_Data').find({product_price: { $gt: 400, $lt: 800 }});

Find the product price which are not between 400 to 600
db.getCollection('Product_Data').find({product_price: {$not: { $gte: 400, $lte: 600 }}});

List the four product which are grater than 500 in price
db.getCollection('Product_Data').find({product_price:{$gt:500}}).limit(4)

Find the product name and product material of each products
db.getCollection('Product_Data').find({},{ product_name: 1, product_material: 1 });

Find the product with a row id of 10
db.getCollection('Product_Data').find({id: '10'});

Find only the product name and product material
db.getCollection('Product_Data').find({},{ product_name: 1, prodduct_material: 1 });

Find all products which contain the value of soft in product material
db.getCollection('Product_Data').find({product_material: 'Soft'});

Find products which contain product color indigo and product price 492.00
db.getCollection('Product_Data').find({$and: [{ product_price: 492 },{ product_color: 'indigo' }]});

Delete the products which product price value are same
db.getCollection("Product_Data").aggregate([
{
$group: {
_id: '$product_price',
count: { $sum: 1 }
}
},
{
$match: {
count: { $gt: 1 }
}
}
]).forEach((e) => {
db.getCollection("Product_Data").deleteMany({ product_price: e._id });
});
