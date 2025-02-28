const express = require("express");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(express.json());


let productosP = [
    {id:1, nombre:"Adobe", precio:500},
    {id:2, nombre:"Cemento", precio:300},
    {id:3, nombre:"Arena de pega", precio:700},
    {id:4, nombre:"Triturado", precio:800},
    {id:5, nombre:"Varilla de 3", precio:200},
    {id:6, nombre:"Tubo pbc", precio:400},
    {id:7, nombre:"Clavos", precio:100}
];

app.get("/",(req,res) => {
    res.send("En curso");
});

app.listen(3000, () => {console.log("Vamos bien...");
});



app.get("/productosP",(req,res) => {
    res.send(productosP);
});

  
app.delete("/productosP/:id",(req,res) =>{
    console.log(req.params);
    const{id}=req.params;
    productos=productosP.filter(p=>p.id != id);
    res.json({mensaje:"producto eliminado",response:productosP});

});

app.post("/productosP",(req,res) => {
    const{ nombre, precio } = req.body;
    const nuevoID = productosP.length > 0 ? productosP[productosP.length - 1].id + 1 : 1;
    const nuevoProducto = { id: nuevoID, nombre, precio };
    productosP.push(nuevoProducto);
    res.json({mensaje:"Producto agregado",response:productosP});
    

});

app.put("/productosp/:id",(req,res) =>{
    const{id} = req.params; 
    const{ nombre, precio } = req.body;
    const producto = productosP.find(p => p.id == id);
    if (producto){
            if (nombre) producto.nombre = nombre;
            if (precio) producto.precio = precio;
    
    res.json({mensaje:"Producto actualizado",response:productosP});
    } else { res.status(404).json({mensaje:"producto no encontrado"})};
});
