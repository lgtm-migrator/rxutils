# `Operator` logError

## logError\<IO>(identifier?: any, logger?: (...args: any[]) => void, loggerThisArg?: any): [MonoTypeOperatorFunction](https://rxjs.dev/api/index/interface/MonoTypeOperatorFunction)\<IO>

A tap() that logs errors. Non-null object errors will not be logged more than once.

| **Parameter** | **Description** | **Type** | **Optional** | **Default value** |
|---------------|-----------------|----------|--------------|-------------------|
| identifier | An optional identifier for the logger. When provided, it'll be passed as the first argument to the logger while the error will come second | <span>any</span> | :heavy_check_mark: Yes |  |
| logger | Logger to use, defaults to console.error | <span>(...args: any[]) => void</span> | No | defaultLoggerFactory() |
| loggerThisArg | If using a custom logger, what to use for "this" when binding a the identifier | <span>any</span> | :heavy_check_mark: Yes |  |

**Example**:
```typescript
import {logError} from '@aloreljs/rxutils/operators';
import {of, throwError, combineLatest} from 'rxjs';

const source1 = throwError(new Error('err')).pipe(
  logError('[source 1 error]')
);
const source2 = of('foo');
const combined = combineLatest(source1, source2).pipe(
  logError('[combined error]')
);
combined.subscribe();
// Outputs [source 1 error] + error object for source 1's error
// Does not output [combined error] [...]
```

*Defined in [operators/logError.ts:103:24](https://github.com/Alorel/rxutils/blob/9057654/projects/rxutils/operators/logError.ts#L103).*