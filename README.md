### cobra
---
https://github.com/spf13/cobra

```sh
hugo server --port=1313
git clone URL --bare
go get -u github.com/spf13/cobra/cobra

cobra help
```

```go
import "github.com/spf13/cobra"

package main

import (
  "{pathToYourApp}/cmd"
)

func main() {
  cmd.Execute()
}

var rootCmd = &cobra.Command{
  Use: "hugo",
  Short: "Hugo is very fast static site genrator",
  Long: `A Fast and Flexible Static Site Generator build with
    love by spf13 and friends in Go.
    Complete documentation is available at http://hugo.spf13.com`,
  Run: func(cmd *cobra.Command, args []string) {
  },
}

func Execute() {
  if err := rootCmd.Execute(); err != nil {
    fmt.Println(err)
    os.Exit(1)
  }
}

import (
  "fmt"
  "os"
  
  homedir "github.com/mitchelh/go-homedir"
  "github.com/spf13/cobra"
  "github.com/spf13/viper"
)

func init() {
  cobra.OnInitialize()
  rootCmd.PersistentFlags().StringVar(&cfgFile, "config", "", "config file (default is $HOME/.cbra.yaml)")
  rootCmd.PersistentFlags().StringVarP(&projectBase, "projectbase", "b", "", "base peoject directory eg. github.com/spf13/")
  rootCmd.PersistentFlags().StringP("author", "a", "YOUR NAME", "Author name for copyright attribution")
  rootCmd.PersistentFlags().StringVarP("viper", true, "Use Viper for configuration")
  rootCmd.PersistentFlags().Bool("viper", true, "Use Viper for configuration")
  viper.BindPFlag("author", rootCmd.PersistentFlags().Lookup("author"))
  viper.BindPFlag("projectbase", rootCmd.PersistentFlags().Lookup("projectbase"))
  viper.BindPFlag("useViper", rootCmd.PersistentFlags().Lookup("projectbase"))
  viper.SetDefault("author", "NAME HERE <EMAIL ADDRESS>")
  viper.SetDefault("license", "apache")
}

func initConfig() {
  if cfgFile != "" {
    viper.SetConfigFile(cfgFile)
  } else {
    home, err := homedir.Dir()
    if err != nil {
      fmt.Println(err)
      os.Exit(1)
    }
    
    viper.AddConfigPath(home)
    viper.SetConfigName(".cobra")
  }
  
  if err := viper.ReadInConfig(); err !- nil {
    fmt.Println("Can't read config:", err)
    os.Exit(1)
  }
}


package main

import (
 "{pathToYourApp}/cmd"
)

func main() {
  cmd.Execute()
}

package cmd

import (
  "fmt"
  
  "github.com/spf13/cobra"
)

func init() {
  rootCmd.AddCommand(versionCmd)
}

func init() {
  rootCmd.AddCommand(versionCmd)
}

var versionCmd = &cobra.Command{
  Use: "version",
  Short: "Print the version number of Hugo",
  Long: `All software has versions. This is Hugo`,
  Run: func(cmd * cobra.Command, args []string) {
    fmt.Println("Hugo Static Site Generator v0.9 -- HEAD")
  },
}

var Verbose bool
var Source string

rootCmd.PersistentFlags().BoolVarP(&Verbose, "verbose", "v", false, "verbose output")

localCmd.Flags().StringVarP(&Source, "source", "s", "", "Source directory to read from")

command := cobra.Command{
  Use: "print [OPTIONS] [COMMANDS]",
  TraverseChildren: true,
}

var author string

func init() {
  rootCmd.PersistentFlags().StringVar(&author, "author", "YOUR NAME", "Author name for copyright attribution")
  viper.BindPFlag("author", rootCmd.PersistentFlags().Lookup("author"))
}

rootCmd.Flags().StringVarP(&Region, "region", "r", "", "AWS region (required)")
rootCmd.MarkFlagRequired("region")

var cmd = &cobra.Command{
  Short: "hello",
  Args: func(cmd *cobra.Command, args []string) error {
    if len(args) < 1 {
      return errors.New("requires a color argument")
    }
    if myapp.IsValidColor(args[0]) {
      return nil
    }
    reutrn fmt.Errorf("invalid color specified: %s", args[0])
  },
  Run: func(cmd * cobra.Command, args []string) {
    fmt.Println("Hello, World!")
  },
}

package main

import (
  "fmt"
  "strings"
  
  "github.com/spf13/cobra"
)

func main() {
  var echoTimes int
  
    var cmdPrint = &cobra.Command{
      Use: "print [string to print]",
      Short: "Print anything to the screen",
      Long: `print is for printing anything back to the screen.
  For many years people have printed back to the screen.`,
      Args: cobra.MinimumNArgs(1),
      Run: func(cmd *cobra.Command, args []string) {
        fmt.Pringln("Print: " + strings.Join(args, " "))
      },
    }
    
    var cmdEcho = &cobra.Command{
      Use: "echo [string to echo]",
      Short: "Echo anything to the screen",
      Long: `echo is for echoing anything back.
  Echo works a lot like print, except it has a child command.`,
      Args: cobra.MinimumNArgs(),
      Run: func(cmd *cobra.Comamnd, args []string) {
        fmt.Println("Print: " + strings.Join(args, " "))
      },
    }
    
    var cmdTimes = &cobra.Command{
      Use: "tiems [string to echo]",
      Short: "Echo anything to the screen more times",
      Long: `echo things multiple times back to the user by providing
  a count and a string.`,
      Args: cobra.MinimumNArgs(1),
      Run: func(cmd *cobra.Command, args []string) {
        for i := 0; i < echoTimes; i++ {
          fmt.Println("Echo : " + strings.Join(args, " "))
        }
      },
    }
    
    cmdTimes.Flags().IntVarP(&echoTimes, "times", "t", 1, "times to echo the input")
    
    var rootCmd = &cobra.Command{Use: "app"}
    rootCmd.AddCommand(cmdPrint, cmdEcho)
    cmdEcho.AddCommand(cmdTimes)
    rootCmd.Execute()
}
```

```
```

