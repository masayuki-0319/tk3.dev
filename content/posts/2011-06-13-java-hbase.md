---
title: Java で HBase にアクセスする
date: 2011-06-13T00:00:00+09:00
slug: f0121784a9cb8d3ecd2baa46a7f3ea806f06249c
---

Java で HBase 上のデータを取得してみる。
設定ファイルを指定してから、データを取得しているだけ。 

久しぶりに Java で書いた気がする。でも、こんな程度だと書いたことに入らないかな。
 
[http://www.ne.jp/asahi/hishidama/home/tech/apache/hbase/java.html:title=HBase Javaメモ(Hishidama's HBase Java Memo)] を参考にしました。

```
import java.io.IOException;

import org.apache.log4j.PropertyConfigurator;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.client.Get;
import org.apache.hadoop.hbase.client.HTableInterface;
import org.apache.hadoop.hbase.client.HTableFactory;
import org.apache.hadoop.hbase.client.Result;
import org.apache.hadoop.hbase.util.Bytes;

public class MyHTable {

    private String tableName;

    Configuration conf;
    HTableFactory factory;
    HTableInterface table;

    public void setTableName(String tableName) {
        this.tableName = tableName;
    }

    public String getTableName() {
        return this.tableName;
    }

    public void configure() {
        this.conf = HBaseConfiguration.create();
    }

    public void configure(String hbaseConf, String log) {
        PropertyConfigurator.configure(log);

        this.conf = HBaseConfiguration.create();
        this.conf.addResource(new Path(hbaseConf));
    }

    public void configure(String hbaseConf) {
        this.conf = HBaseConfiguration.create();
        this.conf.addResource(new Path(hbaseConf));
    }

    public void configure(String log) {
        PropertyConfigurator.configure(log);
    }

    public void connect() {
        this.factory = new HTableFactory();
        this.table = factory.createHTableInterface(this.conf, Bytes.toBytes(this.tableName));
    }

    public void close() {
        factory.releaseHTableInterface(this.table);
    }

    public String[] get(String row, String[] columns) throws IOException {

        String[] values = new String[columns.length];

        Get g = new Get(Bytes.toBytes(row));

        Result r = this.table.get(g);

        for (int i = 0; i < columns.length; i++) {
            String[] params = columns[i].split(":", 2);

            byte[] val_byte = r.getValue(Bytes.toBytes(params[0]), Bytes.toBytes(params[1]));

            values[i] = Bytes.toString(val_byte);
        }

        return values;
    }


    public static void main(String[] args) throws IOException {
        MyHTable table = new MyHTable();

        table.setTableName("app1");

        table.configure("./hbase-site.xml", "./hbase.log4j.properties");
        table.connect();

        String[] columns = {
          "log1:date", "log1:host", "log1:path", "log1:user",
        };

        String[] values = table.get("row1", columns);

        System.out.println("row1 ----");
        for (int i = 0; i < values.length; i++) {
            System.out.println("  [" + columns[i] + "] = " + values[i]);
        }

        table.close();
    }
}

```
