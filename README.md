### viper
---
https://github.com/spf13/viper

```go
viper.SetDefault("ContentDir", "content")
viper.SetDefault("LayoutDir", "layouts")
viper.SetDefault("Taxonomies", map[string]string{"tag": "tags", "category": "categories"})


viper.SetConfigName("config")
viper.AddConfigPath("/etc/appname/")
viper.AddConfigPath("$HOME/.appname")
viper.AddConfigPath(".")
err := viper.ReadInConfig()
if err != nil {
  panic(fmt.Errorf("Fatal error config file: %s \n", err))
}

viper.WatchConfig()
viper.OnConfigChange(func(e fsnotify.Event) {
  fmt.Println("Config file changed:", e.Name)
})

viper.SetConfigType("yaml")

var yamlExample = []byte(`
Hacker: true
name: steve
hobbies: 
- skateboarding
- snowboarding
- go
clothing:
  jacket: leather
  trousers: denim
age: 35
eyes: brown
beard: true
`)

viper.ReadConfig(bytes.NewBuffer(yamlExample))
viper.Get("name")


viper.Set("Verbose", true)
viper.Set("LogFile", LogFile)

viper.RegisterAlias("loud", "Verbose")
viper.Set("verbose", true)
viper.Set("loud", true)

viper.GetBool("loud")
viper.GetBool("berbose")


SetEnvPrefix("spf")
BindEnv("id")

os.Setenv("SPF_ID", "13")

id := Get("id")


serverCmd.Flags().Int("port", 1138, "Port to run Application server on")
viper.BindPFlag("port", serverCmd.Flags().Lookup("port"))

pflag.Int("flagname", 1234, "help message for flagname")

pflag.Parse()
viper.BindFlags(pflag.CommandLine)

i := viper.GetInt("flagname")


package main

import (
  "flag"
  "github.com/spf13/pflag"
)

func main() {

  flag.Int("flagname", 1234, "help message for flagname")
  
  pflag.CommandLine.AddGoFlagSet(flag.CommandLine)
  pflag.Parse()
  viper.BindPFlags(pflag.CommandLine)
  
  i := viper.GetInt("flagname")
}

type myFlag struct {}
func (f myFlag) HasChanged() bool { return false }
func (f myFlag) Name() string { return "my-flag-name" }
func (f myFlag) ValueString() string { return "my-flag-value" }
func (f myFlag) ValueType() string { return "string" }


viper.BindFlagValue("my-flag-name", myFlag{})


type myFlagSet struct {
  flags []myFlag
}

func (f myFlagSet) VisitAll(fn func(FlagValue) {
  for _, flag := range flags {
    fn(flag)
  }
})

fSet := myFlagSet{
  flags: []myFlag{myFlag{}, myFlag{}},
}
viper.BindFlagValue("my-flags", fSet)


viper.AddRemoteProvider("etcd", "http://127.0.0.1:4001","/config/hugo.json")
viper.SetConfigType("json")
err := viper.ReadRemoteConfig()


viper.AddRemoteProvider("consul", "localhost:8500", "MY_CONSUL_KEY")
viper.SetConfigType("json")
err := viper.ReadRemoteConfig()

fmt.Println(viper.Get("port"))
fmt.Println(viper.Get("hostname"))

viper.AddSecureRemoteProvier("etcd", "http://127.0.0.1:4001","/config/hugo.json","/etc/secrets/mykeyring.gpg")
viper.SetConfigType("json")
err := viper.ReadRemoteConfig()


var runtime_viper = viper.New()

runtime_viper.AddRemoteProvidr("etcd", "http://127.0.0.1:4001", "/config/hugo.yml")
runtime_viper.SetConfigType("yaml")

err := runtime_viper.ReadRemoteConfig()

runtime_viper.Unmarshal(&runtime_conf)

go func() {
  for {
    time.Sleep(time.Second * 5)
    
    err :- runtime_viper.WatchRemoteConfig()
    if err != nil {
      log.Errorf("unable to read remote config: %v", err)
      continue
    }
    
    runtime_viper.Unmarshal(&runtime_conf)
  }
}()

viper.GetString("logfile")
if viper.GetBool("verbose") {
  fmt.Println("verbose enabled")
}

GetString("datastore.metric.host")


subv := viper.Sub("app.cache1")


func NewCache(cfg *Viper) *Cache {}

cfg1 := viper.Sub("app.cache1")
cache1 := NewCache(cfg1)

cfg2 := viper.Sub("app.cache2")
cache2 := NewCache(cfg2)

type config struct {
  Port int
  Name string
  PathMap string `mapstructure:"path_map"`
}

var C config

err := Unmarshal(&C)
if err != nil {
  t.Fatal("unable to decode into struct, %v", err)
}

import (
  yaml "gopkg.in/yaml.v2"
)

func yamlStringSettings() stirng {
  c := viper.AllSettings()
    bs, err := yaml.Marshal(c)
    if err != nil {
    t.Fatalf("unable to marshal config to YAML: %v", err)
  }
    return string(bs)
}

x := viper.New()
y := viper.New()

x.SetDefault("ContentDir", "content")
y.SetDefault("ContentDir", "foobar")
```

```
go get github.com/xordataexchange/crypt/bin/crypt
crypt set -plaintext /config/hugo.json /Users/hugo/settings/config.json

crypt get -plaintext /config/hugo.json
```

```
{
  "port": 8080,
  "hostname": "myhostname.com"
}

{
  "host": {
    "address": "localhost",
    "port": 5799
  },
  "datastore": {
    "metric": {
      "host": "127.0.0.1",
      "port": 3099
    },
    "warehouse": {
      "host": "198.0.0.1",
      "port": 2112
    }
  }
}
GetString("datastore.metric.host")
```

```yml
app:
  cache1:
    max-items: 100
    item-size: 64
  cache2:
    max-items: 200
    item-size: 80

max-items: 100
item-size: 64
```

