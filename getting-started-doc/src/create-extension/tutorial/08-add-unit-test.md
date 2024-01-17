# Unit Tests

Finally, let's also add a test for our new request.

In the artifact `hc-example-processing-test` there is an existing test called `HcExampleTransformToUpperCaseTest`. In the same package add a test for the new request:

```java
package hc.tutorial.hc_example.processing;

import static org.assertj.core.api.Assertions.assertThat;

import org.junit.Test;

import com.braintribe.gm.model.reason.Maybe;

import hc.tutorial.hc_example.model.api.HcExampleComputeTextLength;
import hc.tutorial.hc_example.processing.base.HcExampleProcessingTestBase;

/**
 * Processor: {@link HcExampleRequestProcessor}
 * <p>
 * Request: {@link HcExampleComputeTextLength}
 */
public class HcExampleComputeTextLengthTest extends HcExampleProcessingTestBase {

	@Test
	public void testTextLength() throws Exception {
		test(null, 0);
		test("", 0);
		test("hello", 5);
	}

	private void test(String text, int expectedResult) {
		HcExampleComputeTextLength request = HcExampleComputeTextLength.T.create();
		request.setText(text);

		Maybe<Integer> maybeText = request.eval(evaluator).getReasoned();

		assertThat(maybeText.isSatisfied()).isTrue();
		assertThat(maybeText.get()).isEqualTo(expectedResult);
	}

}
```

_**Note:** Feel free to examine the generated classes by yourself. The most important part is the registration of our expert - `HcExampleRequestProcessor` - as the handler for the abstract request type `HcExampleServiceRequest`. This is done in `HcExampleProcessingTestSpace`, method `configureServices(...)` and this ensures all the requests in our tests invoked with `request.eval(evaluator)` are handled by our processor._