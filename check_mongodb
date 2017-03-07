#!/bin/bash

function usage {
  echo "$(basename $0) usage: "
  echo "    -u username Example: root"
  echo "    -p password Example: 1234"
  echo "    -h host Example: localhost"
  echo "    -d database Example: local"
  echo "    -q query Example: db.test.findOne()"
  echo ""
  exit 1
}

while [[ $# -gt 1 ]]
do
  key="$1"
  case $key in
    -u)
    USER="$2"
    shift
    ;;
    -p)
    PASS="$2"
    shift
    ;;
    -h)
    HOST="$2"
    shift
    ;;
    -d)
    DATABASE="$2"
    shift
    ;;
    -q)
    QUERY="$2"
    shift
    ;;
    *)
    usage
    shift
    ;;
  esac
  shift
done

[ ! -z ${HOST} ] && \
[ ! -z ${DATABASE} ] && \
[ ! -z ${QUERY} ] || usage

if [[ ${USER} == "" || ${PASS} == "" ]]
then
  MONGO="$(which mongo) --host ${HOST} ${DATABASE}"
else
  MONGO="$(which mongo) -u ${USER} -p ${PASS} --host ${HOST} ${DATABASE}"
fi

MONGO_CHECK=$(echo "${QUERY}" | ${MONGO})
if [ $? -ne 0 ]
then
  echo "CRITICAL - Failed to execute query ${QUERY} on MongoDB host ${HOST}"
  exit 2
else
  echo "OK - MongoDB"
  exit 0
fi
