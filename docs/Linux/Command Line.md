
## TTY

- http://www.linusakesson.net/programming/tty/
	- Exploring more on how tty works.

--- 

### Cli Functions

#### Generate Password

```bash
function gen_pass() {
    length=${1:?"length must be specified"}
    length=$((length/2))

    dd if=/dev/random bs=1 count=${length} 2>/dev/null | od -An -tx1 | tr -d ' \t\n' ; echo
}
```

#### Matrix like output in shell

```bash

matrix() {
    echo -e "\e[1;40m" ; clear ; while :; do echo $LINES $COLUMNS $(( $RANDOM % $COLUMNS)) $(( $RANDOM % 72 )) ;sleep 0.05; done | awk '{ letters="abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%^&*()"; c=$4;        letter=substr(letters,c,1);a[$3]=0;for (x in a) {o=a[x];a[x]=a[x]+1; printf "\033[%s;%sH\033[2;32m%s",o,x,letter; printf "\033[%s;%sH\033[1;37m%s\033[0;0H",a[x],x,letter;if (a[x] >= $1) { a[x]=0; } }}'
}
```

