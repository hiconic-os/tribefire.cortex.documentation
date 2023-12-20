# Unit Tests

Finally, let's also add a test for our new request.

In the artifact `tf-example-processing-test` there is an existing test called `TfExampleTransformToUpperCaseTest`. In the same package add a test for the new request:

```java
package tf.tutorial.tf_example.processing;

import static org.assertj.core.api.Assertions.assertThat;

import org.junit.Test;

import com.braintribe.gm.model.reason.Maybe;

import tf.tutorial.tf_example.model.api.TfExampleComputeTextLength;
import tf.tutorial.tf_example.processing.base.TfExampleProcessingTestBase;

/**
 * Processor: {@link TfExampleRequestProcessor}
 * <p>
 * Request: {@link TfExampleComputeTextLength}
 */
public class TfExampleComputeTextLengthTest extends TfExampleProcessingTestBase {

	@Test
	public void testTextLength() throws Exception {
		test(null, 0);
		test("", 0);
		test("hello", 5);
	}

	private void test(String text, int expectedResult) {
		TfExampleComputeTextLength request = TfExampleComputeTextLength.T.create();
		request.setText(text);

		Maybe<Integer> maybeText = request.eval(evaluator).getReasoned();

		assertThat(maybeText.isSatisfied()).isTrue();
		assertThat(maybeText.get()).isEqualTo(expectedResult);
	}

}
```

_**Note:** Feel free to examine the generated classes by yourself. The most important part is the registration of our expert - `TfExampleRequestProcessor` - as the handler for the abstract request type `TfExampleServiceRequest`. This is done in `TfExampleProcessingTestSpace`, method `configureServices(...)` and this ensures all the requests in our tests invoked with `request.eval(evaluator)` are handled by our processor._