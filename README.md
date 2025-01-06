

This is a simple Android app that displays a list of recipe categories using Jetpack Compose. The app retrieves categories of recipes and displays them in a grid layout. Each category contains an image and a title.

## Features

- Display a loading indicator while data is being fetched.
- Show error message if an error occurs during data retrieval.
- Display recipe categories in a two-column grid.
- Each category item contains an image and a title.

## Setup

To run this app, you need to have Android Studio installed and set up with the following dependencies:

- Jetpack Compose
- Coil for loading images
- ViewModel for managing UI-related data lifecycle

## Requirements

- Android 5.0 or higher
- Android Studio (with the latest stable version of the Kotlin plugin)
- Jetpack Compose UI toolkit

## Dependencies

Ensure you include the following dependencies in your `build.gradle` files:

gradle

Copy code

`dependencies {     implementation "androidx.compose.ui:ui:1.0.5"     implementation "androidx.compose.material3:material3:1.0.0"     implementation "androidx.lifecycle:lifecycle-viewmodel-compose:2.4.1"     implementation "io.coil-kt:coil-compose:2.1.0" }`

## App Structure

### `RecipeScreen` Composable

This composable handles the overall display of the recipe screen. It checks the current state of the `MainViewModel` and decides whether to display:

- A loading spinner (`CircularProgressIndicator`)
- An error message
- The list of recipe categories

### `CategoryScreen` Composable

The `CategoryScreen` composable takes a list of recipe categories and displays them in a grid using `LazyVerticalGrid`. Each category is represented by a `CategoryItem`.

### `CategoryItem` Composable

Each `CategoryItem` is a column layout that contains:

- An image of the category, loaded using the `Coil` library's `rememberAsyncImagePainter`.
- The category name as a `Text` widget.

### ViewModel Integration

The app uses a `MainViewModel` to manage the state of the recipe categories, which is retrieved from a data source (not provided in this code). It observes the `categoriesState` and updates the UI accordingly.

## Example Usage

kotlin

Copy code

`@Composable fun RecipeScreen(modifier: Modifier = Modifier) {     val recipeViewModel: MainViewModel = viewModel()     val viewState by recipeViewModel.categoriesState      Box(modifier = Modifier.fillMaxSize()) {         when {             viewState.loading -> {                 CircularProgressIndicator(modifier.align(Alignment.Center))             }              viewState.error != null -> {                 Text("Error occurred", modifier.align(Alignment.Center))             }              else -> {                 CategoryScreen(categories = viewState.list)             }         }     } }`

## License

This project is open-source and available under the MIT License. See the LICENSE file for more details.

## Notes

- This app is a simple demonstration of how to use Jetpack Compose for building UIs with dynamic data.
- The `MainViewModel` is assumed to be responsible for fetching and providing the list of recipe categories.
