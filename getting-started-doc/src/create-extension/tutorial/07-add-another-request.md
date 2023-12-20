# Adding Another Request

Let's now add another request and the corresponding expert code. To make it really simple, let's add one which returns the length of given text. 

Only two steps are needed.

1. In our API model (`tf-example-api-model`) we'll add this new request. Let's create a `TfExampleComputeTextLength` in the same package as our existing requests:

```java
package tf.tutorial.tf_example.model.api;

import com.braintribe.model.generic.eval.EvalContext;
import com.braintribe.model.generic.eval.Evaluator;
import com.braintribe.model.generic.reflection.EntityType;
import com.braintribe.model.generic.reflection.EntityTypes;
import com.braintribe.model.service.api.ServiceRequest;

public interface TfExampleComputeTextLength extends TfExampleServiceRequest {
	EntityType<TfExampleComputeTextLength> T = EntityTypes.T(TfExampleComputeTextLength.class);

	String getText();
	void setText(String text);

	@Override
	EvalContext<Integer> eval(Evaluator<ServiceRequest> evaluator);
}
```

2. In our expert implementation (`TfExampleRequestProcessor` in `tf-example-processing`) add the expert method:

```java
private Maybe<Integer> computeTextLength(TfExampleComputeTextLength request) {
    String text = request.getText();

    Integer result = text == null ? 0 : text.length();
    return Maybe.complete(result);
}
```

and make sure to register this new handler in the `configureDispatching` method, which now has two entries:
```java
@Override
protected void configureDispatching(DispatchConfiguration<TfExampleServiceRequest, Object> dispatching) {
    dispatching.registerReasoned(TfExampleTransformToUpperCase.T, (c, r) -> transformToUpperCase(r));
    dispatching.registerReasoned(TfExampleComputeTextLength.T, (c, r) -> computeTextLength(r));
}
```

You can now (re)start `Tomcat` and test this new request. `REST` URL:
```url
http://localhost:8080/tribefire-services/api/v1/tf_example/TfExampleComputeTextLength?&text=hello&accept=application/json
```