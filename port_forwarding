# Go under the root
    # sudo -i

# Enable port forward
    #nano /etc/sysctl.conf
# Change raw
    #net.ipv4.ip_forward = 1
    #sudo sysctl -p


#!/bin/bash
while [[ $# -gt 0 ]]; do
  case $1 in
    -ipf|--ipfrom)
      IPFROM="$2"
      shift 2
      ;;
    -pf|--portfrom)
      PORTFROM="$2"
      shift 2
      ;;
      -ipt| --ipto)
      IPTO="$2"
      shift 2
      ;;
    -pt|--portto)
      PORTTO="$2"
      shift 2
      ;;
    -*|--*)
      echo "Unknown option $1"
      exit 1
      ;;
    *)
      POSITIONAL_ARGS+=("$1")
      shift
      ;;
  esac
done

set -- "${POSITIONAL_ARGS[@]}"

iptables -t nat -I PREROUTING -p tcp -i eth0 --dport ${PORTFROM} -j DNAT --to-destination ${IPTO}:${PORTTO}
iptables -t nat -I POSTROUTING -p tcp -o eth0 --dport ${PORTTO} -d ${IPTO} -j SNAT --to-source ${IPFROM}

iptables -t nat -vnL
