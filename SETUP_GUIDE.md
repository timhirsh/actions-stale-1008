# Maximum PR Generator - Setup & Testing Guide

## 🚀 Quick Setup

The Maximum PR Generator workflow is designed to create as many pull requests as possible while staying within GitHub API limits. Here's how to enable and test it:

### 1. Enable the Workflow

The workflow file has been created at `.github/workflows/generate-pr.yml`. Once you commit and push these changes to your repository, the workflow will be automatically available.

### 2. Test Maximum PR Generation

1. **Navigate to your repository on GitHub**
2. **Go to the "Actions" tab**
3. **Select "Generate Maximum PRs" from the workflow list**
4. **Click "Run workflow" button**
5. **Configure the generation run**:
   - **Batch Size**: 1-50 PRs per matrix job (total = batch_size × 5)

### 3. Maximum Throughput Features

#### 🔄 **Matrix Strategy**
- **5 parallel jobs** run simultaneously
- Each job creates N PRs (configurable batch size)
- **Total PRs per run**: batch_size × 5 matrix jobs
- **Example**: Batch size of 10 = 50 total PRs per workflow run

#### ⏰ **Aggressive Scheduling**
- Runs **every 4 hours** automatically
- Scheduled runs use moderate batch sizes (5 PRs × 5 jobs = 25 PRs)
- Manual runs can use larger batch sizes (up to 50 × 5 = 250 PRs)

#### 🎲 **Random Content Generation**
- **UUID-based filenames** for uniqueness
- **Medium-length lorem ipsum content** (200 words)
- **Text files only** (.txt extension)
- **Root directory placement** for simple organization

#### 🛡️ **API Safety Controls**
- **Rate limit monitoring** with automatic delays
- **Exponential backoff** on API failures
- **Batch processing** to spread API calls over time
- **Retry logic** for failed PR creation

### 4. Generated Content Format

#### 📝 **Text Files (.txt)**
- **Header information**: UUID, timestamp, batch ID
- **Medium-length lorem ipsum**: Fixed 200-word content
- **Simple file structure**: Files created in repository root
- **Unique identifiers**: Each file has a UUID-based filename

### 5. Performance Expectations

#### **Theoretical Maximum (per 4-hour cycle)**
- **API Limit**: 5,000 requests/hour (20,000 per 4-hour cycle)
- **PR Creation Cost**: ~5-10 API calls per PR
- **Estimated Maximum**: 500-1,000 PRs per 4-hour cycle
- **Conservative Target**: 200-300 PRs per 4-hour cycle

#### **Recommended Settings**
- **Manual Testing**: Batch size 5-10 for initial testing
- **Production Load**: Batch size 20-50 for maximum generation
- **Scheduled Runs**: Batch size 5 for sustainable automation

### 6. Monitoring & Debugging

#### **Workflow Summaries**
Each run provides detailed summaries:
- Total PRs generated across all matrix jobs
- API rate limit status
- Success/failure rates
- Batch IDs for cleanup

#### **Branch Naming Convention**
```
auto-gen-{batch-id}-{uuid}
```
- Easy identification of generated branches
- UUID prevents naming conflicts
- Batch ID enables targeted cleanup

### 7. Safety Considerations

⚠️ **Repository Impact**
- Generated PRs are for testing purposes
- Use cleanup workflows regularly
- Monitor repository size growth

⚠️ **API Rate Limits**
- Workflow respects GitHub API limits
- Automatic delays when limits approached
- Exponential backoff on failures

⚠️ **Stale PR Integration**
- Generated PRs do not have special labels
- Generated PRs will be subject to normal stale workflow rules
- Consider manual management of generated PRs

### 8. Quick Start Commands

#### **Test Run (Small Batch)**
```
Workflow: Generate Maximum PRs
Batch Size: 5
```

#### **Maximum Load Test**
```
Workflow: Generate Maximum PRs
Batch Size: 50
```

## 🎯 Expected Results

With the new maximum PR generation approach:
- **25 PRs every 4 hours** (scheduled)
- **Up to 250 PRs per manual run** (50 × 5)
- **~150 PRs per day** from scheduled runs alone
- **1,000+ PRs per day** with manual triggers

The workflow is optimized for maximum throughput while respecting API limits and maintaining repository stability! 🚀
