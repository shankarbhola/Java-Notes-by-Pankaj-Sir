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