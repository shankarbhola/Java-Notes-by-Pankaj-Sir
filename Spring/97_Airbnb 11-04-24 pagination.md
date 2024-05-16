## Pagination ##
* Pagination is a common feature that helps manage large datasets by breaking them into smaller, manageable chunks or pages.
* Spring Data JPA provides an easy and efficient way to implement pagination and sorting. Below is a step-by-step guide to setting up pagination in a Spring Boot application.

![alt text](https://i.ibb.co/YXZGCQH/image.png)

```java
@GetMapping("/all")
    public ResponseEntity<?> getAllProperty(
            @RequestParam(name = "pageSize",defaultValue = "3",required = false) int pageSize,
            @RequestParam(name = "pageNumber",defaultValue = "0",required = false) int pageNumber) {
        Pageable pageable = PageRequest.of(pageNumber,pageSize);
        Page<Property> properties = propertyRepository.findAll(pageable);
        return new ResponseEntity<>(properties, HttpStatus.OK);
    }
```


1. **Default Values:**
   * pageNumber defaults to 0 (first page).
   * pageSize defaults to 10 (10 items per page).

2. **Parameter Annotations:**

   * **@RequestParam(name = "pageSize", defaultValue = "10", required = false)** indicates that **pageSize** is optional, with a default of **10**.
   * **@RequestParam(name = "pageNumber", defaultValue = "0", required = false)** indicates that **pageNumber** is optional, with a default of **0**.
     *  **Default Values:** Typically, pageNumber should default to 0 (the first page) and pageSize should be a positive number (e.g., 10).
     * **Default pageSize:** Setting pageSize to 0 as a default value is not practical because it means fetching 0 items per page, which doesn’t make sense in pagination.

3. **Creating Pageable:**

   * **Pageable pageable = PageRequest.of(pageNumber, pageSize);** correctly creates a **Pageable** object using the provided (or default) **pageNumber** and **pageSize**.
     
     * **Pagination Order:** The conventional order is pageNumber (first) and then pageSize (second) when creating a PageRequest.

4. **Fetching Paginated Results:**

   * **Page<Property> properties = propertyRepository.findAll(pageable);** retrieves the paginated results from the **Property** repository.

* **Returning Response:**

**new ResponseEntity<>(properties, HttpStatus.OK);** wraps the Page object in a ResponseEntity with an HTTP 200 OK status.

5 **Testing the Endpoint**
  * **Default Request: GET /all**
    * Uses pageNumber = 0 and pageSize = 10 by default.
  * **Custom Request: GET /all?pageNumber=2&pageSize=5**
    * Fetches the third page with 5 items per page.

**Response Structure**

```json
{
  "content": [/* list of properties */],
  "pageable": {
    "sort": {
      "sorted": false,
      "unsorted": true,
      "empty": true
    },
    "pageNumber": 0,
    "pageSize": 10,
    "offset": 0,
    "paged": true,
    "unpaged": false
  },
  "totalPages": 5,
  "totalElements": 50,
  "last": false,
  "size": 10,
  "number": 0,
  "sort": {
    "sorted": false,
    "unsorted": true,
    "empty": true
  },
  "numberOfElements": 10,
  "first": true,
  "empty": false
}

```