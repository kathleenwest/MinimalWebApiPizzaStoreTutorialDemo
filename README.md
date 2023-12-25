# PizzaStoreMinimalWebApi

A minimal web api project to showcase basic CRUD operations with Http Verb Operations (Get, Post, Put, and Delete). Swagger documentation is configured for test and verification of the web api. See quick steps and demo code to quickly create a minimal web api with asp.net core and swagger setup. This project code is the result of a Microsoft Learn tutorial to build a web API with minimal API, ASP.NET Core, and .NET.

## How to Quickly Create a Minimal Web Api

### Step #1 - Create web app
```dotnet new web -o PizzaStore -f net8.0```

### Step #2 - Add Routes to Program.cs
Just before app.Run(), add your routes to do stuff. Here is a simple example with a pizza route:
```
app.MapGet("/pizzas/{id}", (int id) => PizzaDB.GetPizza(id));
app.MapGet("/pizzas", () => PizzaDB.GetPizzas());
app.MapPost("/pizzas", (Pizza pizza) => PizzaDB.CreatePizza(pizza));
app.MapPut("/pizzas", (Pizza pizza) => PizzaDB.UpdatePizza(pizza));
app.MapDelete("/pizzas/{id}", (int id) => PizzaDB.RemovePizza(id));
```
### Step #3 - Add Swagger Documentation (Program.cs)
#### Install the Swashbuckle package
```dotnet add package Swashbuckle.AspNetCore --version 6.5.0```
#### Configure Builder Services
```
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo { Title = "PizzaStore API", Description = "Making the Pizzas you love", Version = "v1" });
});
```
#### Configure the app
```
// Change configurations based on environmental settings
// HINT: See Project Properties --> Debug --> Launch Profiles --> Select
// Add ASPNETCORE_ENVIRONMENT = "Development"
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "PizzaStore API V1");
    });
}
```
## Demo Picture
![Swagger Demo](/images/swagger.jpg)
## References

This code is the result of a Microsoft Learn tutorial project: [Build a web API with minimal API, ASP.NET Core, and .NET](https://learn.microsoft.com/en-us/training/modules/build-web-api-minimal-api/)
