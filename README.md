# NeftX

#Say that you have 5 stores and 5 recipes. Assume that all stores are at the same distance from you(travel cost and time are the same to go to multiple stores too). Each recipe has different ingredients. Each store has coupons for different ingredients with their own discount amount. Write code that will display the set of stores that would cost minimum for a recipe.

// Sample data
const stores = [
  { name: 'Store1', discounts: { sugar: 2, flour: 3, butter: 1, eggs: 1.5, milk: 1 } },
  { name: 'Store2', discounts: { sugar: 1.5, flour: 2, butter: 1, eggs: 2, milk: 1.5 } },
  { name: 'Store3', discounts: { sugar: 2, flour: 2.5, butter: 1.2, eggs: 1.5, milk: 1.8 } },
  { name: 'Store4', discounts: { sugar: 1.8, flour: 3, butter: 0.8, eggs: 1.3, milk: 2 } },
  { name: 'Store5', discounts: { sugar: 2.5, flour: 2.2, butter: 1, eggs: 1.6, milk: 1.2 } }
];

// Sample recipe (quantity of ingredients needed)
const recipe = { sugar: 3, flour: 2, butter: 1, eggs: 4, milk: 2 };

// Function to calculate the total cost of a recipe at a store
function calculateCost(store, recipe) {
  let totalCost = 0;
  
  for (let ingredient in recipe) {
    // Ensure the store has a discount for the ingredient
    if (store.discounts[ingredient]) {
      totalCost += store.discounts[ingredient] * recipe[ingredient];
    }
  }
  
  return totalCost;
}

// Function to find the store(s) with the minimum cost
function findCheapestStore(stores, recipe) {
  let minCost = Infinity;
  let cheapestStores = [];
  
  // Calculate the cost for each store and track the minimum cost
  stores.forEach(store => {
    const cost = calculateCost(store, recipe);
    if (cost < minCost) {
      minCost = cost;
      cheapestStores = [store.name]; // Start a new list of cheapest stores
    } else if (cost === minCost) {
      cheapestStores.push(store.name); // Add to the list if the cost is the same
    }
  });
  
  return cheapestStores;
}

// Example usage:
const cheapestStores = findCheapestStore(stores, recipe);
console.log(`The cheapest store(s) for the recipe are: ${cheapestStores.join(', ')}`);
