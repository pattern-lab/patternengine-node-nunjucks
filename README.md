[📢 Archived in favor of https://github.com/pattern-lab/patternlab-node](https://github.com/pattern-lab/patternlab-node)

# The Nunjucks engine for Pattern Lab / Node

## Installing

To install the Nunjucks engine in your edition, run `npm install patternengine-node-nunjucks`.

## Supported features
- [x] [Includes](http://patternlab.io/docs/pattern-including.html)
- [x] Lineage
- [x] [Hidden Patterns](http://patternlab.io/docs/pattern-hiding.html)
- [x] [Pseudo-Patterns](http://patternlab.io/docs/pattern-pseudo-patterns.html)
- [x] [Pattern States](http://patternlab.io/docs/pattern-states.html)
- [ ] [Pattern Parameters](http://patternlab.io/docs/pattern-parameters.html) (Accomplished instead using native Nunjucks variables)
- [ ] [Style Modifiers](http://patternlab.io/docs/pattern-stylemodifier.html) (Accomplished instead using native Nunjucks variables)

Level of Support is more or less full. Partial calls and lineage hunting are supported. Nunjucks does not support the mustache-specific syntax extensions, style modifiers and pattern parameters, because their use cases are addressed by the core Nunjucks feature set. Pattern Lab's listitems feature is still written in the mustache syntax.

## Extending the Nunjucks instance

To add custom filters or make customizations to the nunjucks instance, create a file named `patternlab-nunjucks-config.js` in the root of your Pattern Lab project. `patternlab-nunjucks-config.js` should export a function that takes two parameters. The first parameter is the nunjucks instance; the second is the nunjucks instance's environment.

```
module.exports = function (nunjucks, env) {
  [YOUR CUSTOM CODE HERE]
};
```

Example: `patternlab-nunjucks-config.js` file that uses lodash and adds three custom filters.
```
var _shuffle = require('lodash/shuffle'),
  _take = require('lodash/take');

exports = module.exports = function (nunjucks, env) {
  env.addFilter('shorten', function (str, count) {
    return str.slice(0, count || 5);
  });

  env.addFilter('shuffle', (arr) => {
    return _shuffle(arr);
  });

  env.addFilter('take', (arr, number) => {
    return _take(arr, number);
  });
};
```

## What Nunjucks features are missing?

I have not yet figured out a way to support variables in pattern includes. I'm thinking it might be possible to use Nunjucks precompile feature to get the compiled partial name before returning it to Pattern Lab, but just a thought at this point.
