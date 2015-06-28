# Joining CharStreams
CharStreams.join方法可以处理InputSupplier实例并组合他们，使得他们在逻辑上看起来像是一个InputSupplier实例。
```
    @Test
    public void joinTest() throws Exception {
        File f1 = new File("src/main/resources/sampleTextFileOne.txt");
        File f2 = new File("src/main/resources/sampleTextFileTwo.txt");
        File f3 = new File("src/main/resources/lines.txt");
        File joinedOutput = new File("src/test/resources/joined.txt");
        joinedOutput.deleteOnExit();

        List<InputSupplier<InputStreamReader>> inputSuppliers = getInputSuppliers(f1,f2,f3);
        InputSupplier<Reader> joinedSupplier = CharStreams.join(inputSuppliers());
        OutputSupplier<OutputStreamWriter> outputSupplier = Files.newWriterSupplier(joinedOutput, Charsets.UTF_8);
        String expectedOutputString = joinFiles(f1,f2,f3);
        CharStreams.copy(joinedSupplier,outputSupplier);
        String joinedOutputString = joinFiles(joinedOutput);
        assertThat(joinedOutputString,is(expectedOutputString));
    }

    private String joinFiles(File ...files) throws IOException {
        StringBuilder builder = new StringBuilder();
        for (File file : files) {
            builder.append(Files.toString(file,Charsets.UTF_8));
        }
            return builder.toString();
        }

    private List<InputSupplier<InputStreamReader>> getInputSuppliers()(File ...files){
        List<InputSupplier<InputStreamReader>> list = Lists.newArrayList();
        for (File file : files) {
            list.add(Files.newReaderSupplier(file,Charsets.UTF_8));
        }
        return list;
    }
```
1. 我们建立四个文件对象，三个用于join，一个用于输出文件。
2. 我们使用一个私有的工具类getInputSuppliers()，调用Files.newReaderSupplier静态工厂方法来为每一个资源文件建立InputSupplier对象。
3. 然后，我们建立组合多个InputSupplier为逻辑上一个的InputSupplier。
4. 通过把第四个文件传递给Files.newWriterSupplier工厂方法，建立OutputSupplier。
5. 我们使用另一个私有工具方法，joinFiles，调用每个资源的Files.toString方法为测试做准备。
6. 调用CharStreams.copy方法，写每个InputSuppliers的内容到OutputSupplier。
7. 验证是否目标文件的内容和原始一样。
