# Lexical-Scoping
# Create a new environment to store cached results
cache <- new.env()

# Define the function that will use caching
cached_mean <- function(x) {
  # Check if the result is already cached
  if (exists("result", envir = cache) && identical(cache$result$input, x)) {
    message("Returning cached result")
    return(cache$result$value)
  } else {
    message("Computing mean")
    # Calculate the mean
    result <- mean(x)
    # Store the result in the cache
    cache$result <- list(input = x, value = result)
    return(result)
  }
}

# Test the cached_mean function
vec1 <- c(1, 2, 3, 4, 5)
vec2 <- c(6, 7, 8, 9, 10)

# First call (not cached)
print(cached_mean(vec1))  # Output: Computing mean, 3

# Second call (cached)
print(cached_mean(vec1))  # Output: Returning cached result, 3

# Different input (not cached)
print(cached_mean(vec2))  # Output: Computing mean, 8
