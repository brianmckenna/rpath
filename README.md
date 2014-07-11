rpath
=====

install rpath module
```
pip install https://github.com/brianmckenna/rpath/archive/master.zip
```

NOTE: the package is currently called xpath despite the repo name, will handle this shortly so `import rpath` works, for now, must `import xpath`

```python
import xpath

exprs = [
    "/foobar('Deployment')/child::asset_attrs[child::s_name='foo']", # fails
    "/child::resource('Deployment')/child::asset_attrs[child::s_name='foo']",
    "/resource('Deployment')/asset_attrs[s_name='foo']",
    "/child::resource()[child::name='myMooring']/target::association('hasDevice')", # note 'target' instead of object (object is reserved word in Python)
    "/resource()[name='myMooring']/target::association('hasDevice')",
    "self::resource()[child::name='CTD_Simulator']/child::asset_attrs/child::s_name/child::value[fn:position=1]",
    "/CTD_Simulator/asset_attrs/s_name/value[1]", # caution, what is intended with /CTD_Simulator/ I think in ION "name=" is synonymous with child node
    "/name='CTD_Simulator'/asset_attrs/s_name/value[fn:position=1]",
    "self::node()/child::resource/child::asset_attrs/child::s_name/child::value[fn:position=1]",
    "resource/asset_attrs/s_name/value[1]",
    "/subject::resource('Deployment')/asset_attrs[s_name='foo']",
]

for expr in exprs:
    xpath.validate(expr)
```
