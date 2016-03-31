# quiz
Short quiz:
 1. Look into new JEP274 API.
 2. Explain what the foolowing code does?
 
 public static MyClass {
 
     public static boolean less(int i, int cnt) {
        return i<=cnt;
    }

    public static void main(String[] args) throws Throwable {


        MethodHandle mhLoop = MethodHandles.loop(
                new MethodHandle[]{
                        MethodHandles.dropArguments(MethodHandles.constant(int.class, 1), 0, int.class),
                        MethodHandles.insertArguments(
                                MethodHandles.lookup().findStatic(Integer.class, "sum", MethodType.methodType(int.class, int.class, int.class)), 1 , 1),
                        MethodHandles.dropArguments(MethodHandles.dropArguments(MethodHandles.dropArguments(
                                MethodHandles.lookup().findStatic(MyClass.class, "less", MethodType.methodType(boolean.class, int.class, int.class)), 1, int.class), 1, int.class), 1, int.class),
                        MethodHandles.dropArguments(MethodHandles.dropArguments(MethodHandles.dropArguments(MethodHandles.dropArguments(
                                MethodHandles.identity(int.class), 0, int.class), 0, int.class), 3, int.class), 3, int.class)
                },
                new MethodHandle[]{
                        null,
                        MethodHandles.dropArguments(MethodHandles.dropArguments(
                                MethodHandles.lookup().findStatic(Integer.class, "sum", MethodType.methodType(int.class, int.class, int.class)), 0, int.class), 0, int.class),
                        null,
                        null
                },
                new MethodHandle[]{
                        MethodHandles.constant(int.class, 1),
                        MethodHandles.dropArguments(MethodHandles.dropArguments(MethodHandles.dropArguments(
                                MethodHandles.identity(int.class), 0, int.class), 0, int.class), 0, int.class),
                        null,
                        null
                },
                new MethodHandle[]{
                        MethodHandles.constant(int.class, 1),
                        MethodHandles.dropArguments(MethodHandles.identity(int.class), 0, int.class),
                        null,
                        null
                });

        System.out.println((int)mhLoop.invokeExact(8));
    }


}