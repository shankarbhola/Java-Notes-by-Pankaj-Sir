**Page Sorting**

```java
@GetMapping("/all")
    public ResponseEntity<?> getAllProperty(
            @RequestParam(name = "pageNumber",defaultValue = "0",required = false) int pageNumber,
            @RequestParam(name = "pageSize",defaultValue = "3",required = false) int pageSize,
            @RequestParam(name = "sortBy", defaultValue = "id", required = false) String propertyName,
            @RequestParam(name = "sortDir", defaultValue = "asc", required = false) String sortDir
            ) {

        // Determine sort direction
        Sort.Direction direction = sortDir.equalsIgnoreCase("desc") ? Sort.Direction.DESC : Sort.Direction.ASC;
        // Create Sort object
        Sort sort = Sort.by(direction, propertyName);
        // Create Pageable object with sorting
        Pageable pageable = PageRequest.of(pageNumber, pageSize, sort);
        Page<Property> properties = propertyRepository.findAll(pageable);
        return new ResponseEntity<>(properties, HttpStatus.OK);
    }
```
1. **Parameter**
   * **sortBy:** Specifies the field to sort by (defaults to "id").
   * **sortDir:** Specifies the sort direction ("asc" for ascending, "desc" for descending, defaults to "asc").
2. Sort Direction:

* **Sort.Direction direction = sortDir.equalsIgnoreCase("desc") ? Sort.Direction.DESC : Sort.Direction.ASC;** determines the sort direction based on the sortDir parameter. 

3. **Sort and Pageable Objects:**

* **Sort sort = Sort.by(direction, sortBy);** creates a Sort object with the specified field and direction.
* **Pageable pageable = PageRequest.of(pageNumber, pageSize, sort);** creates a Pageable object incorporating pagination and sorting.

4. **Testing the Endpoint**
   * **Default Request: GET /all**
     * Uses default values: pageNumber = 0, pageSize = 3, sortBy = "id", sortDir = "asc".
   * **Custom Request: GET /all?pageNumber=0&pageSize=5&sortBy=nightlyPrice&sortDir=desc**
     * Fetches the second page with 5 items per page, sorted by name in descending order.


**Response Structure**
```JSON
{
  "content": [/* list of properties */],
  "pageable": {
    "sort": {
      "sorted": true,
      "unsorted": false,
      "empty": false
    },
    "pageNumber": 1,
    "pageSize": 5,
    "offset": 5,
    "paged": true,
    "unpaged": false
  },
  "totalPages": 10,
  "totalElements": 50,
  "last": false,
  "size": 5,
  "number": 1,
  "sort": {
    "sorted": true,
    "unsorted": false,
    "empty": false
  },
  "numberOfElements": 5,
  "first": false,
  "empty": false
}

```