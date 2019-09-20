# remove-null-empty
SpringBoot microservice which supports removal of null and empty and json media type values from the response

In this lession we will learn how to remove null and empty values from both xml and json response.

For Enabling XML and JSON support Please refer to this repo( https://github.com/surajpjannu/json-xml-support.git)

```aidl
import com.fasterxml.jackson.annotation.JsonInclude;
import com.fasterxml.jackson.databind.ObjectMapper;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.MediaType;
import org.springframework.http.converter.HttpMessageConverter;
import org.springframework.http.converter.json.MappingJackson2HttpMessageConverter;
import org.springframework.http.converter.xml.MappingJackson2XmlHttpMessageConverter;
import org.springframework.web.servlet.config.annotation.ContentNegotiationConfigurer;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

import java.util.List;

@Configuration
@EnableWebMvc
public class JsonXmlSupportConfiguration implements WebMvcConfigurer {

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

}
```

Import RemoveNullAndEmpty.postman_collection.json in postman and test the API's.

# Test 1

Request
```aidl
http://localhost:8080/employees.json
```
Response
```aidl
[
    {
        "firstName": "Suraj",
        "middleName": "Panduranga",
        "lastName": "Jannu",
        "age": 26,
        "salary": 100000
    },
    {
        "firstName": "Pramod",
        "lastName": "Jannu",
        "age": 29,
        "salary": 300000
    },
    {
        "firstName": "Mohan",
        "lastName": "Mari",
        "age": 49,
        "salary": 200000
    },
    {
        "firstName": "Abhilash",
        "age": 34,
        "salary": 400000
    },
    {
        "firstName": "Harsha",
        "age": 28,
        "salary": 500000
    },
    {
        "firstName": "Imran",
        "age": 26,
        "salary": 800000
    }
]
```


# Test 2

Request
```aidl
http://localhost:8080/employees.xml
```
Response
```aidl
<List>
    <item>
        <firstName>Suraj</firstName>
        <middleName>Panduranga</middleName>
        <lastName>Jannu</lastName>
        <age>26</age>
        <salary>100000.0</salary>
    </item>
    <item>
        <firstName>Pramod</firstName>
        <lastName>Jannu</lastName>
        <age>29</age>
        <salary>300000.0</salary>
    </item>
    <item>
        <firstName>Mohan</firstName>
        <lastName>Mari</lastName>
        <age>49</age>
        <salary>200000.0</salary>
    </item>
    <item>
        <firstName>Abhilash</firstName>
        <age>34</age>
        <salary>400000.0</salary>
    </item>
    <item>
        <firstName>Harsha</firstName>
        <age>28</age>
        <salary>500000.0</salary>
    </item>
    <item>
        <firstName>Imran</firstName>
        <age>26</age>
        <salary>800000.0</salary>
    </item>
</List>
```