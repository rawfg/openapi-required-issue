# openapi-required-issue

Despite the OpenAPI definition sets the `required` property to `true` of the `requestBody` section:

```yaml
      requestBody:
        required: true
        description: File image
        content:
          multipart/form-data:
            schema:
              properties:
                file:
                  type: string
                  format: binary
            encoding:
              file:
                contentType: image/png, image/jpeg
```

The generated API sets the `required` to `false`:

```java
@Generated(value = "org.openapitools.codegen.languages.SpringCodegen", date = "2023-09-11T18:32:21.447767+02:00[Europe/Warsaw]")
@Validated
public interface UploadApi {

    /**
     * PUT /upload/{id}/file
     *
     * @param id ID (required)
     * @param file  (optional)
     * @return Uploaded (status code 204)
     *         or Not Found (status code 404)
     */
    @RequestMapping(
            method = RequestMethod.PUT,
            value = "/upload/{id}/file",
            consumes = { "multipart/form-data" }
    )
    ResponseEntity<Void> putFile(
            @Pattern(regexp = "\\\\d{4}")  @PathVariable("id") String id,
            @RequestPart(value = "file", required = false) MultipartFile file
    );

}
```