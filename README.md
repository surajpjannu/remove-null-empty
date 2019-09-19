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