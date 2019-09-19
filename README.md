# remove-null-empty
SpringBoot microservice which supports removal of null and empty and json media type values from the response

In this lession we will learn how to remove null and empty values from both xml and json response.

For Enabling XML and JSON support Please refer to this repo( https://github.com/surajpjannu/json-xml-support.git)

```aidl
    @Override
    public void extendMessageConverters(List<HttpMessageConverter<?>> converters) {
        for (HttpMessageConverter converter : converters) {
            if (converter instanceof MappingJackson2HttpMessageConverter) {
                final ObjectMapper mapper = ((MappingJackson2HttpMessageConverter) converter).getObjectMapper();
                mapper.setSerializationInclusion(JsonInclude.Include.NON_EMPTY);
            } else if (converter instanceof MappingJackson2XmlHttpMessageConverter) {
                final ObjectMapper mapper = ((MappingJackson2XmlHttpMessageConverter) converter).getObjectMapper();
                mapper.setSerializationInclusion(JsonInclude.Include.NON_EMPTY);
            }
        }
    }
```

Import RemoveNullAndEmpty.postman_collection.json in postman and test the API's.