# casbin-v3-bun-adapter

```go
casbinModel := casbinv3Model.Model{}
casbinModel.LoadModelFromText(`
[request_definition]
r = sub, dom, obj, act

[policy_definition]
p = sub, dom, obj, act, eft

[role_definition]
g = _, _, _

[policy_effect]
e = some(where (p.eft == allow)) && !some(where (p.eft == deny))

[matchers]
m = g(r.sub, p.sub, r.dom) && (r.dom == p.dom || keyMatch(r.dom, p.dom)) && r.obj == p.obj && r.act == p.act
	`)

a, err := casbinbun.NewAdapterWithBunDB([BUN_DB])
_ = a.LoadPolicy(casbinModel)
enforcer, _ := casbinv3.NewEnforcer(casbinModel, a)

```

## Credits
https://github.com/JunNishimura/casbin-bun-adapter