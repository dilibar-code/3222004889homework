# 3222004889homework
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class PaperCheck {

    public static void main(String[] args) {
        String filePath1 = "D:/test files/orig.txt";
        String filePath2 = "D:/test files/orig_0.8_add.txt";
        String resultFilePath = "D:/test files/result.txt";

        try {
            String content1 = readTxt(filePath1);
            String content2 = readTxt(filePath2);

            double similarity = getSimilarity(content1, content2);

            writeTxt(resultFilePath, "两篇论文的相似度为：" + similarity);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static double getSimilarity(String str1, String str2) {
        // 这里可以使用更复杂的算法，比如余弦相似度等
        // 简单示例，计算相同字符的比例
        int sameCount = 0;
        for (int i = 0; i < str1.length() && i < str2.length(); i++) {
            if (str1.charAt(i) == str2.charAt(i)) {
                sameCount++;
            }
        }
        return (double) sameCount / Math.max(str1.length(), str2.length());
    }

    public static String readTxt(String filePath) throws IOException {
        StringBuilder content = new StringBuilder();
        try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = br.readLine())!= null) {
                content.append(line).append("\n");
            }
        }
        return content.toString();
    }

    public static void writeTxt(String filePath, String content) throws IOException {
        try (FileWriter writer = new FileWriter(filePath)) {
            writer.write(content);
        }
    }
}
