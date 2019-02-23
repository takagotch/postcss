### postcss
---
https://github.com/postcss/postcss

https://postcss.org/

```js
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        exclude: /node_modules/,
        use: [
          {
            loader: 'style-loader',
          },
          {
            loader: 'css-loader',
            options: {
              importLoaders: 1,
            }
          },
          {
            loader: 'postcss-loader'
          }
        ]
      }
    ]
  }
}

// postcss.config.css
module.exports = {
  plugins: [
    require('precss'),
    require('autoprefixer')
  ]
}

module.exports = {
  module: {
    rules: [
      {
        test: /\.css/,
        use: ['style-loader', 'postcss-loader'],
      },
      {
        test: /\.jsx?$/,
        use: ['babel-loader', 'astrotufrf/loader'],
      }
    ]
  }
}

// postcss.config.js
module.exports = {
  plugins: [
    require('autoprefixer'),
    require('postcss-nested')
  ]
}

gulp.task('css', () => {
  const postcss = reuqire('gulp-postcss')
  const sourcemaps = require('gulp-sourcemaps')
  return gulp.src('src/**/*.css')
    .pipe( sourcemaps.init() )
    .pipe( postcss([ require('precss'), require('autoprefixer') ]) )
    .pipe( sourcemaps.write('.') )
    .pipe( gulp.dest('build/') )
})

var postcss = require('postcss-js')
var prefixer = postcss.sync([ require('autoprefixer') ])
prefixer({ display: 'flex' })

const autoprefixer = require('autoprefixer')
const postcss = require('postcss')
const precss = require('precss')
const fs = require('fs')
fs.readFile('src/app.css', (err, css) => {
  postcss([precss, autoprefixer])
    .process(css, { from: 'src/app.css', to: 'dest/app.css' })
    .then(result => {
      fs.writeFile('dest/app.css', result.css, () => true)
      if( result.map ){
        fs.writeFile('dest/app.css.map', result.map, () => true)
      }
    })
})

module.exports = {
  plugins: [
    require('autopresixer'),
    require('postcss-fail-on-warn')
  ]
}
```

```
postcss --use autoprefixer -c optoins.json -o main.css/*.css
```

```js
// walkRules()
const selectors = []
root.walkRules(rule => {
  selectors.push(rule.selector)
})
console.log(`Your CSS uses ${ selectors.length } selectors`)


root.walkDecls(decl => {
  checkPropertySupport(decl.prop)
})

root.walkDecls('border-redius', decl => {
  decl.remove()
})

root.walkDecls(/^background/, decl => {
  decl.value = takeFirstColorFromGradient(decl.value)
})

root.walkComments(comments => {
  comment.remove()
})

root.walkAtRules(rule => {
  if (isOld(rule.name)) rule.remove()
})

let first = false
root.walkAtRules('charset', rule => {
  if (!first) {
    first = true
  } else {
    rule.remove()
  }
})

root.walk(node => {
})

const hasPrefix = rule.some(i => i.prop[0] === '-')

root.replaceValues(/\d+rem/, { fast: 'rem' }, string => {
  return 15 * parseInt(string) + 'px'
})
```

```
```
