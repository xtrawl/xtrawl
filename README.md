<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Shop Every Language</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <h1>Welcome to the Ultimate Shopping Platform</h1>
    <div class="cart">Cart: <span id="cart-count">0</span> items</div>
  </header>
  <section id="products-list">
    <!-- Dynamic product list generated by JS -->
  </section>
  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  padding: 20px;
}

header {
  background-color: #333;
  color: white;
  padding: 10px;
  text-align: center;
}

.cart {
  margin-top: 10px;
  font-size: 1.2em;
}

#products-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
  margin-top: 30px;
}

.product {
  border: 1px solid #ddd;
  padding: 10px;
  text-align: center;
}

.product button {
  background-color: #4CAF50;
  color: white;
  padding: 10px;
  border: none;
  cursor: pointer;
}

.product button:hover {
  background-color: #45a049;
}
const products = [
  { id: 1, name: "JavaScript for Beginners", price: 10 },
  { id: 2, name: "Python Masterclass", price: 15 },
  { id: 3, name: "Learn C++", price: 20 },
];

const productsList = document.getElementById("products-list");
const cartCount = document.getElementById("cart-count");

let cart = [];

function updateCart() {
  cartCount.innerText = cart.length;
}

function addToCart(productId) {
  cart.push(products.find((p) => p.id === productId));
  updateCart();
}

function renderProducts() {
  productsList.innerHTML = products
    .map(
      (product) => `
      <div class="product">
        <h3>${product.name}</h3>
        <p>$${product.price}</p>
        <button onclick="addToCart(${product.id})">Add to Cart</button>
      </div>`
    )
    .join("");
}

renderProducts();
from flask import Flask, jsonify, request

app = Flask(__name__)

products = [
    {"id": 1, "name": "JavaScript for Beginners", "price": 10},
    {"id": 2, "name": "Python Masterclass", "price": 15},
    {"id": 3, "name": "Learn C++", "price": 20},
]

@app.route("/products", methods=["GET"])
def get_products():
    return jsonify(products)

if __name__ == "__main__":
    app.run(debug=True)
const express = require('express');
const app = express();

const products = [
  { id: 1, name: "JavaScript for Beginners", price: 10 },
  { id: 2, name: "Python Masterclass", price: 15 },
  { id: 3, name: "Learn C++", price: 20 }
];

app.get('/products', (req, res) => {
  res.json(products);
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
class ProductsController < ApplicationController
  def index
    @products = [
      { id: 1, name: "JavaScript for Beginners", price: 10 },
      { id: 2, name: "Python Masterclass", price: 15 },
      { id: 3, name: "Learn C++", price: 20 }
    ]
    render json: @products
  end
end
use Illuminate\Support\Facades\Route;

Route::get('/products', function () {
    return response()->json([
        ['id' => 1, 'name' => 'JavaScript for Beginners', 'price' => 10],
        ['id' => 2, 'name' => 'Python Masterclass', 'price' => 15],
        ['id' => 3, 'name' => 'Learn C++', 'price' => 20]
    ]);
});
package main

import (
	"encoding/json"
	"fmt"
	"log"
	"net/http"
)

type Product struct {
	ID    int    `json:"id"`
	Name  string `json:"name"`
	Price int    `json:"price"`
}

var products = []Product{
	{ID: 1, Name: "Go Programming", Price: 10},
	{ID: 2, Name: "Master Rust", Price: 15},
	{ID: 3, Name: "Scala for the win", Price: 20},
}

func getProducts(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	json.NewEncoder(w).Encode(products)
}

func main() {
	http.HandleFunc("/products", getProducts)
	fmt.Println("Server starting at http://localhost:8080")
	log.Fatal(http.ListenAndServe(":8080", nil))
}
use rocket::{get, launch, routes};
use rocket_contrib::json::Json;

#[derive(serde::Serialize)]
struct Product {
    id: i32,
    name: String,
    price: i32,
}

#[get("/products")]
fn get_products() -> Json<Vec<Product>> {
    Json(vec![
        Product { id: 1, name: "Rust Programming", price: 10 },
        Product { id: 2, name: "Go Masterclass", price: 15 },
        Product { id: 3, name: "Java Developer Kit", price: 20 },
    ])
}

#[launch]
fn rocket() -> _ {
    rocket::build().mount("/", routes![get_products])
}
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import java.util.List;

@SpringBootApplication
public class ShoppingApp {
    public static void main(String[] args) {
        SpringApplication.run(ShoppingApp.class, args);
    }
}

@RestController
class ProductController {
    @GetMapping("/products")
    public List<Product> getProducts() {
        return List.of(
            new Product(1, "Java Mastery", 20),
            new Product(2, "Scala Advanced", 30),
            new Product(3, "Swift for iOS", 40)
        );
    }
}

class Product {
    private int id;
    private String name;
    private int price;

    // Constructor, getters, and setters...
}
import akka.actor.ActorSystem
import akka.http.scaladsl.Http
import akka.http.scaladsl.server.Directives._
import akka.stream.ActorMaterializer
import spray.json._

case class Product(id: Int, name: String, price: Int)

object ProductJsonProtocol extends DefaultJsonProtocol {
  implicit val productFormat = jsonFormat3(Product)
}

object Main extends App {
  import ProductJsonProtocol._

  implicit val system = ActorSystem()
  implicit val materializer = ActorMaterializer()

  val route =
    path("products") {
      get {
        complete {
          HttpEntity(ContentTypes.`application/json`, 
            Seq(
              Product(1, "Functional Programming in Scala", 20),
              Product(2, "Learn Akka", 25)
            ).toJson.prettyPrint)
        }
      }
    }

  Http().newServerAt("localhost", 8080).bind(route)
}
import Vapor

struct Product: Content {
    var id: Int
    var name: String
    var price: Int
}

func routes(_ app: Application) throws {
    app.get("products") { req -> [Product] in
        return [
            Product(id: 1, name: "Learn Swift", price: 15),
            Product(id: 2, name: "Advanced iOS Development", price: 25)
        ]
    }
}

public func configure(_ app: Application) throws {
    try routes(app)
}
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class ProductController extends Controller
{
    public function index()
    {
        return response()->json([
            ['id' => 1, 'name' => 'PHP Basics', 'price' => 10],
            ['id' => 2, 'name' => 'Advanced Laravel', 'price' => 20]
        ]);
    }
}
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/products', methods=['GET'])
def get_products():
    products = [
        {'id': 1, 'name': 'Python for Beginners', 'price': 10},
        {'id': 2, 'name': 'Advanced Flask', 'price': 20}
    ]
    return jsonify(products)

if __name__ == '__main__':
    app.run(debug=True)
class ProductsController < ApplicationController
  def index
    render json: [
      { id: 1, name: "Ruby for the Win", price: 10 },
      { id: 2, name: "Learn Ruby on Rails", price: 20 }
    ]
  end
end
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;

namespace ShoppingApp.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class ProductsController : ControllerBase
    {
        [HttpGet]
        public IEnumerable<Product> GetProducts()
        {
            return new List<Product>
            {
                new Product { Id = 1, Name = "C# Fundamentals", Price = 10 },
                new Product { Id = 2, Name = "Advanced .NET", Price = 20 }
            };
        }
    }

    public class Product
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public int Price { get; set; }
    }
}
const express = require('express');
const app = express();

const products = [
  { id: 1, name: "Node.js Basics", price: 10 },
  { id: 2, name: "Learn Express", price: 15 }
];

app.get('/products', (req, res) => {
  res.json(products);
});

app.listen(3000, () => {
  console.log("Server running on http://localhost:3000");
});
