  

export function Product({ id, name, price, onAddToCart }){  
  
    return (  
        <div className="product">  
            <div>name :{ name } </div>  
            <div>cost : { price } </div>  
            <button onClick={() => onAddToCart(id)}>Add to cart</button>  
        </div>    );  
  
}








import { Product } from "./Product.jsx"  
  
export function ProductList({products , onAddToCart}){  
  
    return products.map((product)=> {  
        return <Product {...product} key={product.id} onAddToCart={onAddToCart} />  
    })  
  
      
}









import { ProductList } from "./ProductList.jsx";  
import { Cart } from "./Cart.jsx";  
  
export function ShoppingCartApp(){  
  
  
    const products = [  
        { id: 1, name: 'Product 1', price: 10 },  
        { id: 2, name: 'Product 2', price: 15 },  
        { id: 3, name: 'Product 3', price: 20 },  
    ];  
  
  
  
  
    return(  
        <>  
            <h1>Products</h1>  
            <div className="product-list">  
                <ProductList products={products}/>  
            </div>            <div className="cart">  
                <Cart/>            </div>  
        </>    )  
}

