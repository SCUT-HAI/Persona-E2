<template>
  <div class="table-section">
    <el-row justify="center">
      <el-col :xs="24" :sm="22" :md="20" :lg="18">
        <h2 class="md-h2" style="text-align: center;">Cognitive Soundness (Win-Rate)</h2>
        <p class="md-p" style="text-align: center;">
          We evaluated the cognitive plausibility of the psychological reasoning process.
        </p>
        
        <div class="table-wrapper">
          <div class="table-responsive">
            <table class="academic-table">
              <thead>
                <tr>
                  <th style="text-align: left;">Model</th>
                  <th>Consistency (BFI)</th>
                  <th>Plausibility (BFI)</th>
                  <th>Specificity (BFI)</th>
                </tr>
              </thead>
              <tbody>
                <tr><td style="text-align: left;">GPT5.1</td><td><b>78.8</b></td><td><b>70.4</b></td><td><b>68.9</b></td></tr>
                <tr><td style="text-align: left;">Llama3</td><td>70.8</td><td>55.4</td><td>61.3</td></tr>
                <tr><td style="text-align: left;">Qwen3</td><td>70.2</td><td>59.9</td><td>56.9</td></tr>
                <tr><td style="text-align: left;">Gemma3</td><td>67.8</td><td>63.1</td><td>65.0</td></tr>
                <tr><td style="text-align: left;">Ministral3</td><td>72.0</td><td>58.9</td><td>65.5</td></tr>
              </tbody>
            </table>
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.md-h2 { font-size: 1.5rem; font-weight: 600; color: #333; margin-bottom: 0.75rem; font-family: inherit; }
.md-p { font-size: 1.1rem; line-height: 1.6; color: #555; margin-bottom: 1.5rem; font-family: inherit; }

.table-wrapper { display: flex; justify-content: center; width: 100%; }
.table-responsive { max-width: 100%; overflow-x: auto; }
.academic-table { border-collapse: collapse; text-align: center; font-family: "Times New Roman", Times, serif; font-size: 15px; min-width: 60%; margin: 0 auto; }
.academic-table th, .academic-table td { padding: 10px 20px; border-bottom: 1px solid #ddd; }
.academic-table thead tr { border-top: 2px solid #000; border-bottom: 1px solid #000; }
.academic-table tbody tr:last-child { border-bottom: 2px solid #000; }
</style>