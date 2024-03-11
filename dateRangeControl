import React, { Component } from 'react';
import { connect } from 'react-redux';
import { RootState } from 'reducers';
import styles from './datepicker.scss';

// imported actions
import { changeDateRange, changeDatepickerView } from 'actions/dateRange';

// imported functions
import { renderChipIcon } from 'utils/datepicker';

// imported components
import Datepicker from 'components/datepicker';
import DatepickerChipTooltip from 'components/datepickerChipTooltip';

const MONTH_NAMES = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];

// props passed from store
const mapStateToProps = (state: RootState): Props_1 => ({
    startDate: state.app.startDate,
    endDate: state.app.endDate,
    datepickerView: state.app.datepickerView
});

// actions
const mapDispatchToProps: Props_2 = {
    changeDateRange: changeDateRange
};

// interfaces
export interface Props_1 {
    startDate?: string;
    endDate?: string;
    datepickerView: string;
}

export interface Props_2 {
    changeDateRange: (startDate: string, endDate: string) => void;
}

export type PropsFinal = Props_1 & Props_2;

// dateRageControl component that renders header with latest selected date information
// and input or datepicker component to select new dates based on selected view
export class DateRangeControl extends Component<PropsFinal> {

    // chipColor is red when no endDate is selected and green when endDate is selected
    public chipColor: string = 'red';
    constructor(props: any) {
        super(props);
    }

    componentDidUpdate() {
        if (this.props.endDate) {
            this.chipColor = 'green';
        } else {
            this.chipColor = 'red';
        }
    }

    componentShouldUpdate(prevProps: PropsFinal) {
        if (prevProps.endDate === this.props.endDate && prevProps.startDate === this.props.startDate) {
            return false;
        }
    }

    render() {
        // render seleced dates via inputs
        if (this.props.datepickerView === 'view_1') {
            const Title = this.props.endDate ? 'Start & End Date selected' : 'No date selected';
            console.log(Title);
            return (
                <div>
                    <div className={styles.datepicker_title}>{Title}</div>
                    <div className={styles.datepicker_startDate}>{this.props.startDate ? MONTH_NAMES[new Date(this.props.startDate).getMonth()] : '' }</div>
                    <div className={styles.datepicker_separator}>-</div>
                    <div className={styles.datepicker_endDate}>{this.props.endDate ? MONTH_NAMES[new Date(this.props.endDate).getMonth()] : '' }</div>
                    <button onClick={changeDatepickerView()} style={{color: blue}}/>Change view</button>
                    <DatepickerInput />
                </div >
            );
        }

        // render seleced dates via datepicker      
        if (this.props.datepickerView === 'view_2') {
            const Title = this.props.endDate ? 'Start & End Date selected' : 'No date selected';
            const chip_display = this.props.endDate ? true : false;
            return (
                <div>
                <div className={styles.datepicker_title}>{Title}</div>
                <div className={styles.datepicker_startDate}>{this.props.startDate ? MONTH_NAMES[new Date(this.props.startDate).getMonth()] : '' }</div>
                <div className={styles.datepicker_separator}>-</div>
                <div className={styles.datepicker_endDate}>{this.props.endDate ? MONTH_NAMES[new Date(this.props.endDate).getMonth()] : '' }</div>
                <button onClick={changeDatepickerView()} style={{color: blue}}/>Change view</button>
                <Datepicker onClick={changeDateRange} />

                {
                chip_display ?
                    <DatepickerChipTooltip startDate={this.props.endDate}>
                        <div className={this.chipColor === 'red' ? styles.redChip : styles.greenChip}>
                            <div>{renderChipIcon(this.props.endDate)}</div>
                            <div>
                                {this.props.endDate ? 'You havent selected end date' : 'You selected end date'}
                            </div>
                        </div>
                    </DatepickerChipTooltip> : <div></div>
            }

                </div >
            );
        }

    }
}

export type DatepickerInputType = {
    changeDateRange: changeDateRange;
}
// input component where you can write and submit new dates
export const DatepickerInput = (props: DatepickerInputType) => {
    const [startDateInputValue, setStartDateInputValue] = React.useState("");
    const [endDateInputValue, setEndDateInputValue] = React.useState("");

    const handleStartDateInputChange = (event) => {
        setStartDateInputValue(event.target.value);
    };

    const handleEndDateInputChange = (event) => {
        setEndDateInputValue(event.target.value);
    };

    return (
        <>
            <input type="text" value={''} onChange={handleStartDateInputChange} />
            <input type="text" value={''} onChange={handleEndDateInputChange} />
            <button onClick={changeDateRange(startDateInputValue, endDateInputValue)}>Set new dates</button>
        </>
    )
};

export default connect(mapStateToProps, mapDispatchToProps)(DateRangeControl);