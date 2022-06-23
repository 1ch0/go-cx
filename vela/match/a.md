# 

```go
	for _, rule := range in.Rules {
		match := func(src []string, val string) (found bool) {
			for _, _val := range src {
				found = found || _val == val
			}
			return val != "" && found
		}
		if (match(rule.Selector.CompNames, manifest.GetName()) && match(rule.Selector.ResourceTypes, manifest.GetKind())) ||
			(rule.Selector.CompNames == nil && match(rule.Selector.ResourceTypes, manifest.GetKind()) ||
				(rule.Selector.ResourceTypes == nil && match(rule.Selector.CompNames, manifest.GetName()))) {
			return rule.Strategy
		}
	}
```